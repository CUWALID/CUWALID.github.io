---
title: "StoPET Tutorial"
layout: single
permalink: /tutorials/stopet-tutorial/

sidebar:
  nav: "tutorials"
---

<a href="/model-info/stopet-model" class="btn btn--primary">Model Information</a>

## Running the model

To run the StoPET model you can use the code below:

```python
from cuwalid.stopet.main_stopet import run_stoPET

run_stoPET("input.json")
```

Or run from the terminal using this command:

```bash
# replace "input.json" with the path to your input json
python -m cuwalid.stopet.main_stopet input.json
```

StoPET's parameter files are too large to be included inside the package, if you are yet to install them please use this command in your terminal:
```bash
python -m cuwalid.tools.download_data
```


Once this script runs it will produce all the required folders in the `root_outputpath`,  
with new folders being created as `result_R<trial>` (e.g. `result_R0`, `result_R1`, …).  
Within each folder, there will be other folders containing the NetCDF files.  
These are the files required to do the forecasting.

Next, we run the forecast generation. This will also use the same JSON input you just used to get the required variables, navigate through the folders created before, and do the forecasting.  
The final NetCDF files will be stored in a folder called `ensemble_forecast`, which will be created in the `root_outputpath`.

To run the forecast in your code you can use the code below:

```python
from cuwalid.stopet.forecast_generation_v2 import run_pet_forecast

run_pet_forecast("input.json")
```

Or from the command line using this command:

```bash
# replace "input.json" with the path to your input json
python -m cuwalid.stopet.forecast_generation_v2 input.json
```

## Input Parameters

The best way to build the input files for StoPET is to use the [**Input Helper**](/tools/input-helper/).  
Here you can find an easy-to-use interface to create the file and others with clear descriptions.

Here are the parameters used for the StoPET model:

- **execution_type**: `"hpc"`  
  Can be set to `"dryp"` or `"hpc"`. `"dryp"` completes the trials in a loop, while `"hpc"` runs one trial at a time (useful for batch jobs).

- **outputpath**: `"stopet_output"`  
  Directory where model output will be saved.

- **runtype**: `"regional"`  
  Can be `"regional"` or `"single"`—determines whether PET is generated for a point or area.

- **startyear**: `2024`  
  Start year for PET time series.

- **endyear**: `2024`  
  End year for PET time series.

- **seasonswitch**: `1`  
- **startdate**: `274`  
- **enddate**: `365`  
- **seasonName**: `"OND"`  
  Seasonal Julian date range.

- **latval**: `3.8`  
- **lonval**: `36.6`  
  Latitude/longitude for single-point PET.

- **latval_min**: `-5.5`  
- **latval_max**: `-4.5`  
- **lonval_min**: `33.0`  
- **lonval_max**: `34.5`  
  Bounding box for regional PET.

- **locname**: `"HAD"`  
  Used in the filename of the final PET result.

- **number_ensm**: `3`  
  Number of ensemble runs per realization. **Must be divisible by 3.**

- **tempAdj**: `3`  
  Method for temperature adjustment:  
  `1`, `2`, or `3`. Refer to the paper for details.

- **deltat**: `1.5`  
  Expected temperature increase (used only if `tempAdj = 2`).

- **udpi_pet**: `5`  
  Percentage increase in PET (used only if `tempAdj = 1`).

- **slice_only**: `6`  
  PET slicing mode:  
  `0` = run full PET year + slice;  
  `1` = slice only (if full PET already run).

- **tercile_forecast_file**: `"ICPAC_TempF_OND2022_HAD.nc"`  
  Path to ICPAC seasonal tercile temperature forecast file.
