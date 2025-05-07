---
title: "Running in a HPC Tutorial"
layout: single
permalink: /tutorials/hpc-tutorial/

sidebar:
  nav: "tutorials"
---

# CUWALID Forecast Workflow Guide

This guide describes how to run the full CUWALID forecasting workflow, including generating JSON input files and submitting jobs to a compute cluster. This example uses `qsub` but it can adjusted to whichever software your hpc uses.

---

##  1. Generate JSON Files and Bash Scripts

Run the JSON generator script which also creates `.bash` job scripts:

```bash
python -m cuwalid.tools.generate_json.py cuwalid_config.json
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

Run the bash generator script:

an example is provided below of how you can do this, but it will depend on your environment

```python 
import os

def write_bash(job_name, command, logname=None):
    path = f"bSub_runMe/cuwalid_run_{job_name}.bash"
    log_file = logname or f"{job_name}.log"
    lines = [
        "#!/bin/bash\n",
        f"#$ -N cuwalid_{job_name}\n",
        "#$ -l h_rt=01:00:00\n",
        "#$ -l h_vmem=4G\n",
        "#$ -pe smp 1\n",
        "#$ -cwd\n",
        "#$ -j y\n",
        "#$ -V\n",
        "#$ -S /bin/bash\n",
        "\n",
        "source ~/miniconda3/bin/activate\n",
        "conda activate cwld\n",
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

## 3. Submit the Workflow

Make sure your JSON lists (`storm_jsons.txt`, `stopet_jsons.txt`, and `dryp_jsons.txt`) are in the root or properly pathed in the script.

Then you can run a bash file like this:

```bash
#!/bin/bash
set -e

# Navigate to the directory with .bash files
pushd bSub_runMe

# Read Storm JSON files and submit jobs for each
while IFS= read -r storm_json; do
    # Submit Storm job
    storm_jobid=$(qsub -v STORM_JSON="$storm_json" cuwalid_run_storm.bash | awk '{print $3}')
    
    # Submit StoPET job for the same JSON (without holding Storm job)
    stopet_json=$(echo "$storm_json" | sed 's/storm/stopet/')  # Assuming stopet json has the same name as storm json, just changed "storm" -> "stopet"
    stopet_jobid=$(qsub -v STOPET_JSON="$stopet_json" cuwalid_run_stopet.bash | awk '{print $3}')
    
    # Now submit DRYP jobs after Storm and StoPET (they should hold until both jobs are done)
    while IFS= read -r dryp_json; do
        # Create a DRYP job script for each DRYP JSON
        job_name=$(basename "$dryp_json" .json)
        bash_script="bSub_runMe/dryp_${job_name}.bash"

        cat <<EOF > "$bash_script"
#!/bin/bash
#$ -N dryp_${job_name}
#$ -l h_rt=01:00:00
#$ -l h_vmem=4G
#$ -pe smp 1
#$ -cwd
#$ -j y
#$ -V
#$ -S /bin/bash

source ~/miniconda3/bin/activate
conda activate cwld

# Run DRYP model with the provided JSON path
python -m cuwalid.dryp "$dryp_json" > bSub_logMe/dryp_${job_name}.log 2>&1
EOF

        chmod +x "$bash_script"

        # Submit the DRYP job, which depends on both Storm and StoPET jobs
        qsub -hold_jid $storm_jobid,$stopet_jobid "$bash_script"
    done < path/to/dryp_jsons.txt  # Path to your dryp_jsons.txt
done < path/to/storm_jsons.txt  # Path to your storm_jsons.txt

popd

```

This script will:
- Loop through each Storm JSON and submit `cuwalid_run_storm.bash`
- Submit corresponding `cuwalid_run_stopet.bash` job **in parallel**
- Generate and submit DRYP jobs that depend on both Storm and StoPET jobs completing

Each DRYP JSON file will get its own dynamically generated bash script in `bSub_runMe/`.

---

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

- Make sure you have `qsub` and `conda` properly configured on your HPC environment.
- Activate the `cwld` environment in your scripts.
- Double-check file paths in your `config.json` and script logic.
- If needed, modify memory/time parameters in `.bash` headers.

---
```
