---
title: "Running in a HPC Tutorial"
layout: single
permalink: /tutorials/hpc-tutorial/

sidebar:
  nav: "tutorials"
---

# CUWALID Forecast Workflow Guide

This guide describes how to run the full CUWALID forecasting workflow, including generating JSON input files and submitting jobs to a compute cluster. This example uses `SLURM` but it can adjusted to whichever software your hpc uses.

You can find some examples script to generate .bash files and submitting jobs in the the following repo:
<a href="https://github.com/AndresQuichimbo/CUWALID-tutorials/tree/main/input_template/HPC" target="_blank" class="btn btn--primary">
    <img src="/assets/images/icons/github-mark.svg" alt="GitHub" class="icon"> CUWALID HPC Templates
</a>



---

##  1. Generate JSON Files and Bash Scripts

Before you start running cuwalid, make sure you have created and have access to all parameter datasets as well as model parameter and setting files for each of the components that you are planning to run.

You can either use the **[Input Helper](/tutorial/input-helper-tutorial) tool** to create all files required to for all components or you can find some templates in the following repo:
<a href="https://github.com/AndresQuichimbo/CUWALID-tutorials/tree/main/input_template" target="_blank" class="btn btn--primary">
    <img src="/assets/images/icons/github-mark.svg" alt="GitHub" class="icon"> CUWALID Templates
</a>


Run the JSON generator script which also creates `.bash` job scripts:

```bash
python -m cuwalid.tools.generate_json your_cuwalid_config.json
```

This will:
- Parse the configuration
- Generate STORM, StoPET, and DRYP input JSONs
- Save lists of generated files:
  - `storm_jsons.txt`
  - `stopet_jsons.txt`
  - `dryp_jsons.txt`
- complete some necessary pre-processing needed for storm and stopet

---
## 2. Create the Bash Job Templates

### Submit independent jobs (option 1)

Alternatively, after the JSON files have been generated, you may find convinient to submit cuwalid jobs separately for each componet instead of running all component at the same time. This may help you to keep control of each component of the forecasting system.

You can find in the following link a set of scripts to submit jobs separately:

<a href="https://github.com/AndresQuichimbo/CUWALID-tutorials/tree/main/input_template/HPC" target="_blank" class="btn btn--primary">
    <img src="/assets/images/icons/github-mark.svg" alt="GitHub" class="icon"> CUWALID HPC Templates
</a>

The following file can be used as templates to submit the climatological componets: [STORM and stoPET](https://github.com/AndresQuichimbo/CUWALID-tutorials/blob/main/input_template/HPC/submit_meteo_jobs_slurm.bash):
- `submit_meteo_jobs_slurm.bash`

whereas for the hydrological components the following file can be used to to submit jobs: [DRYP](https://github.com/AndresQuichimbo/CUWALID-tutorials/blob/main/input_template/HPC/submit_dryp_jobs_slurm.bash).
- `submit_dryp_jobs_slurm.bash`


---

### Create the Bash Job Templates (option 2)

Run the bash generator script:

an example is provided below of how you can do this, but it will depend on your environment

```python 
import os

def write_bash(job_name, command, logname=None, slurm=True, memory="4G", time="01:00:00"):
    """Writes a bash script for submitting a job to a cluster.
    
    Parameters:
    ----------
    time : str
        The maximum time the job is allowed to run, in the format HH:MM:SS.
    memory : str
        The amount of memory allocated for the job, e.g., "4G" for 4 gigabytes.
    job_name : str
        The name of the job.
    command : str
        The command to run in the job.
    logname : str, optional
        The name of the log file. If not provided, defaults to job_name.log.
    """

    path = f"bSub_runMe/cuwalid_run_{job_name}.bash"
    log_file = logname or f"{job_name}.log"
    lines = [
            "#!/bin/bash\n",
            f"#SBATCH --job-name=cuwalid_{job_name}\n",
            f"#SBATCH --time={time}\n",
            f"#SBATCH --mem={memory}\n",
            "#SBATCH --cpus-per-task=1\n",
            "#SBATCH --output=../bSub_logMe/%x.log\n",
            "#SBATCH --error=../bSub_logMe/%x.err\n",
            "\n",
            "module load miniconda3\n",
            "source activate cwld\n",
            f"{command} > ../bSub_logMe/{log_file} 2>&1\n"
            ]
    with open(path, "w") as f:
        f.writelines(lines)

def main():
    os.makedirs("bSub_runMe", exist_ok=True)
    os.makedirs("bSub_logMe", exist_ok=True)

    # Only run STORM and StoPET jobs, since post-processing is now integrated
    write_bash("storm", "python -m cuwalid.storm.main_storm input_storm.json")
    write_bash("stopet", "python -m cuwalid.stopet.main_stopet_wrapper input_stopet.json")

    # Dryp jobs are generated separately later
    print("Run `submit_all.sh` after generating dryp_jsons.txt.")

if __name__ == "__main__":
    main()
```

---

#### Submit the Workflow

Make sure your JSON lists (`storm_jsons.txt`, `stopet_jsons.txt`, and `dryp_jsons.txt`) are in the root or properly pathed in the script.

Then you can run a bash file like this:

```bash
#!/bin/bash
set -e

# Navigate to the directory with .bash files
pushd bSub_runMe

# Read Storm JSON files and submit jobs for each
while IFS= read -r storm_json; do
    # Submit Storm job and get job ID
    storm_jobid=$(sbatch --export=STORM_JSON="$storm_json" --parsable cuwalid_run_storm.bash)

    # Submit StoPET job for the same JSON
    stopet_json=$(echo "$storm_json" | sed 's/storm/stopet/')
    stopet_jobid=$(sbatch --export=STOPET_JSON="$stopet_json" --parsable cuwalid_run_stopet.bash)

    # Now submit DRYP jobs after Storm and StoPET (they should wait until both are done)
    while IFS= read -r dryp_json; do
        job_name=$(basename "$dryp_json" .json)
        bash_script="bSub_runMe/dryp_${job_name}.bash"

        cat <<EOF > "$bash_script"
#!/bin/bash
#SBATCH --job-name=dryp_${job_name}
#SBATCH --time=01:00:00
#SBATCH --mem=4G
#SBATCH --cpus-per-task=1
#SBATCH --output=bSub_logMe/dryp_${job_name}.log
#SBATCH --error=bSub_logMe/dryp_${job_name}.log
#SBATCH --export=ALL

source ~/miniconda3/bin/activate
conda activate cwld

python -m cuwalid.dryp "$dryp_json"
EOF

        chmod +x "$bash_script"

        # Submit the DRYP job with dependency on both Storm and StoPET
        sbatch --dependency=afterok:$storm_jobid:$stopet_jobid "$bash_script"
    done < path/to/dryp_jsons.txt

done < path/to/storm_jsons.txt

popd


```
or download this CUWALID [SLURM-type](https://github.com/AndresQuichimbo/CUWALID-tutorials/blob/main/input_template/HPC/submit_cuwalid_jobs_qsub.bash) file from the following link or a CUWALID [QSUB-type](https://github.com/AndresQuichimbo/CUWALID-tutorials/blob/main/input_template/HPC/submit_cuwalid_jobs_slurm.bash)

This script will:
- Loop through each Storm JSON and submit `cuwalid_run_storm.bash`
- Submit corresponding `cuwalid_run_stopet.bash` job **in parallel**
- Generate and submit DRYP jobs that depend on both Storm and StoPET jobs completing

Each DRYP JSON file will get its own dynamically generated bash script in `bSub_runMe/`.


---

## 3. Complete forecasting

Because this system use the same file structure as the main cuwalid system, to complete the final forecasting steps after dryp you can simply run the normal cuwalid.This can be done be running main_cuwalid script with a cuwalid_input.json. **[Here](/tutorials/cuwalid_tutorial)** you can find all information required to run CUWALID. In the configuration file, you need enable the WaterCast conmponens by activating the `HydroCast` and `IMCast` components. But please insure you have disabled the **running of storm, stopet and dryp** in the configurations settings. 

## Job Dependencies

Job dependencies are managed with `-hold_jid`:
- DRYP jobs wait for both STORM and StoPET jobs to finish
- STORM and StoPET run **in parallel**

---

## Logs

All logs will be saved in `bSub_logMe/`, including:
- `storm_*.log`
- `stopet_*.log`
- `dryp_*.log`

---

## Final Notes

- Make sure you have `SLURM` or `qsub` and `conda` properly configured on your HPC environment.
- Activate the `cwld` environment in your scripts.
- Double-check file paths in your `config.json` and script logic.
- If needed, modify memory/time parameters in `.bash` headers.

---
```
