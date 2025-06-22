---
title: "Storm Tutorial"
layout: single
permalink: /tutorials/storm-tutorial/

sidebar:
  nav: "tutorials"
---

<a href="/model-info/storm-model" class="btn btn--primary">Model Information</a>


## Running the model

**IMPORTANT**: GDAL is needed to be able to run Storm. This cannot be added to the package because it does not work with the Windows operating system.  
You will need to install this yourself. If you are using a conda environment, you can run this:

```bash
conda install gdal
```

To run the Storm model you can use the code below:

```python
from cuwalid.storm.main_storm import run_storm

run_storm("input.json")
```

Or run from the terminal using this command:

```bash
# replace "input.json" with the path to your input json
python -m cuwalid.storm.main_storm input.json
```

## Input Parameters

The best way to build the input files for storm is to use the [**Input Helper**](/tools/input-helper/). Here you can find an easy to use interface to create the file and others with clear descriptions.

Here are the parameters used for the Storm model:

- **NUMSIMS**: `2`  
  The number of simulation runs per season. Each simulation generates one NetCDF file.

- **NUMSIMYRS**: `1`  
  The number of years to simulate for each run. This indicates how long the simulation will run.

- **SEASON_TAG**: `"OND"`  
  The tag identifying the seasonal period of the simulation.

- **SEED_YEAR**: `2024`  
  The year in which the simulation will start.

- **PDF_FILE**: `"./model_input/ProbabilityDensityFunctions.csv"`  
  The path to the Probability Density Functions CSV file, which contains the statistical parameters for the simulation.

- **SHP_FILE**: `"./model_input/HAD_basin.shp"`  
  The path to the shapefile representing the catchment area. This file should be in WGS84 format.

- **DEM_FILE**: `"./model_input/HAD_wgs84.tif"`  
  The path to the Digital Elevation Model (DEM) raster file. This is optional but required if running simulations at different altitudes.

- **ZON_FILE**: `"./model_input/regions.shp"`  
  The path to the shapefile that defines the regions for the simulation.

- **TER_FILE**: `"./model_input/tercilesICPAC_OND_2024.shp"`  
  The path to the shapefile containing tercile information for seasonal forecasts (typically from ICPAC or similar providers).

- **OUT_PATH**: `"./storm_output_test/"`  
  The directory where the output files from the simulation will be saved.
