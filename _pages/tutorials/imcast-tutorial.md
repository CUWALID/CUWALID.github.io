---
title: "ImCast Tutorial"
layout: single
permalink: /tutorials/imcast-tutorial/

sidebar:
  nav: "tutorials"
---

<a href="/model-info/imcast-model" class="btn btn--primary">Model Information</a>

## Running the model

Plotting maps using cuwalid forecasting is done by running this command in the terminal:

```bash
# replace "input.json" with the path to your input json
python -m cuwalid.forecasting.main_impact_forecast input.json
```

Or you can import the function into your code like this:

```python
from cuwalid.forecasting.main_impact_forecast import plot_maps_json

# replace "input.json" with the path to your input json
plot_maps_json("input.json")
```

## Input Parameters

The best way to build the input files for forecast impact is to use the [**Input Helper**](/tools/input-helper/).  
Here you can find an easy-to-use interface to create the file and others with clear descriptions.

Here are the parameters used for the Forecast Impact model:

- **plot_scales**: List of geographical scales for plotting (e.g., `["County", "Zoom"]`).

- **country_name**: Country to generate forecast for (e.g., `"Kenya"`).

- **place_names**: List of specific regions or counties of interest (e.g., `["Samburu", "Laikipia", "Meru"]`).

- **seasons**: Forecast season (e.g., `"OND"` or `"MAM"`).

- **water_status**: Type of water-related event being forecasted (e.g., `"Flood"`).

- **year**: The year of the forecast (e.g., `2022`).

- **language**: Language for the output (e.g., `"English"`).

- **output_dir**: Directory for saving outputs (e.g., `"output"`).

- **netcdf_path**: Path to the NetCDF forecast dataset. Use `'YYYY'` in the filename to represent the selected year dynamically.

- **threshold_path**: Path to the threshold file. Use `'SSS'` in the filename to represent the selected season dynamically. Do **not** include `_flow_quantiles.nc` or `_quantiles.nc` in the name — these will be added automatically by the script.

- **mask_path**: Path to the mask file used to limit forecast region.

- **river_path**: Path to river network data for hydrological features.

- **shape_path**: Optional path to custom shapefile to override built-in HAD region shapefiles.

### Optional (auto-generate netcdf/threshold paths instead of specifying them directly)

- **prev_output_path**: Directory from previous model run that contains the output NetCDF files (e.g., `"forecasting_dataset/HAD/output/"`).

- **pp_path**: Post-processing threshold files path (e.g., `"forecasting_dataset/HAD/postpp/"`).

- **model_name**: The model name used during forecasting (to help script construct file names correctly).

⚠️ **Note**: If both `netcdf_path` and `threshold_path` are provided, they take priority over the automatically generated paths using `prev_output_path`, `pp_path`, and `model_name`.
