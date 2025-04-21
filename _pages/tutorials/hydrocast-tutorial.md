---
title: "HydroCast Tutorial"
layout: single
permalink: /tutorials/hydrocast-tutorial/

sidebar:
  nav: "tutorials"
---

<a href="/model-info/hydrocast-model" class="btn btn--primary">Model Information</a>

## Running the model

Plotting hydrological forecast is done by running this command in the terminal:

```bash
# replace "input.json" with the path to your input json
python -m cuwalid.forecasting.main_hydro_forecast input.json
```

Or you can import the function into your code like this:

```python
from cuwalid.forecasting.main_hydro_forecast import run_hydro_forecast

# replace "input.json" with the path to your input json
run_hydro_forecast("input.json")
```

## Input Parameters

The best way to build the input files for hydrological forecasting is to use the [**Input Helper**](/tools/input-helper/).  
Here you can find an easy-to-use interface to create the file and others with clear descriptions.

Here are the parameters used for the Forecast Hydrological model:

- **run_hindcast**: Boolean — Set to `true` to enable the hindcast simulation.

- **run_forecast**: Boolean — Set to `true` to enable the forecast simulation.

- **run_plotting**: Boolean — Set to `true` to generate plots from the forecast and hindcast simulations.

- **hindcast_model_name**: Name of the model used for the hindcast, e.g., `"HAD_IMERGba_sim0"`.

- **forecast_model_name**: Name of the forecast model, e.g., `"MAM_2022_realization_test"`.

- **model_path**: Path to where the model outputs (hindcast and forecast) are stored.

- **postpp_path**: Path to the post-processing directory (used after running simulations).

- **threshold_path**: Path to a NetCDF file with threshold values (e.g., for classifying flood/drought conditions). Use placeholders like `YYYY` for dynamic year substitution.

- **dataset_path**: Path to the dataset directory, usually containing observational or gridded inputs.

- **season**: List of seasons (e.g., `["MAM"]` for March-April-May).

- **start_year**: Integer — Start year for the simulation.

- **end_year**: Integer — End year for the simulation.

- **variables**: A dictionary of variables to include in the simulation. Each is a boolean (`true` or `false`):

  - **pre**: Precipitation  
  - **pet**: Potential Evapotranspiration  
  - **aet**: Actual Evapotranspiration  
  - **tht**: Total Heat  
  - **egw**: Groundwater Evaporation  
  - **inf**: Infiltration  
  - **run**: Surface Runoff  
  - **rch**: Recharge  
  - **fch**: Flow from Catchment  
  - **gdh**: Groundwater Depth  
  - **dis**: Discharge  
  - **tls**: Total Land Surface Temperature  
  - **wte**: Water Table Elevation  
  - **twsc**: Terrestrial Water Storage Change  
  - **wrsi**: Water Requirement Satisfaction Index
