## Cuwalid Tutorial

This tutorial is to help you run the entire cuwalid system

learn more infomation about the system **[here](/model-info/#cuwalid-system)**

### Models

These are the different models found in the cuwalid system

- **[DRYP](/model-info/#dryp-model)** – Description
- **[StoPET](/model-info/#stopet-model)** – Description 
- **[Storm](/model-info/#storm-model)** – Description
- **[WaterCast](/model-info/#watercast-model)** – Description
- **[ImCast](/model-info/#imcast-model)** – Description 


### Preparing Your System for Running CUWALID

**IMPORTANT:** GDAL is needed to run STORM. This **cannot** be included in the package because it is not fully compatible with Windows.  
You will need to **install it manually**. If you are using a **Conda environment**, you can install it using:

```bash
conda install gdal "numpy<2.0"
```

---

**IMPORTANT:** For running **stoPET**, you need to **download additional parameter files**.  
The system will give you a warning if you try to run it without these files.

Run the following command to download them:

```bash
# If using CUWALID as a PyPi package:
python -m cuwalid.tools.download_data

# If using CUWALID from GitHub:
python cuwalid/tools/download_data.py
```

---

### Running the Models

To run the models in CUWALID, use the following **Python script**:

```python
from cuwalid.main_cuwalid import run_cuwalid

run_cuwalid("cuwalid_input.json")
```

Alternatively, you can **run it from the terminal**:

```bash
# Replace "cuwalid_input.json" with the path to your input JSON file
python -m cuwalid.main_cuwalid cuwalid_input.json
```

---

### Input for CUWALID

The CUWALID input file is a **combined JSON file** containing all the necessary configurations for each model (e.g., DRYP, stoPET, STORM).  
For details on each parameter, refer to the individual model tutorials.

An example **CUWALID input JSON file** looks like this:

```json
{
    "run_STORM": true,
    "run_stoPET": true,
    "run_DRYP": true,
    "run_WaterCast": false,
    "sim_in_parallel": false,
    "historical": {
        "model_name": "historical_model",
        "main_path": "/path/to/historical/data",
        "model_path": "/path/to/model/outputs",
        "postpp_path": "/path/to/post_processing_outputs"
    },
    "forecasting": {
        "forecasting_model_name": "forecast_model",
        "Tercile_Pre_path": "/path/to/precipitation/netcdf",
        "Tercile_Tem_path": "/path/to/temperature/netcdf",
        "threshold_path": "/path/to/threshold/data",
        "season": ["OND"],
        "start_year": 2000,
        "end_year": 2025,
        "year": 2025,
        "NSIM": 10
    }
}
```

---

### Parameter Descriptions

#### **General Settings**
- **`run_STORM`** *(Boolean)* – Whether to run the STORM simulation (`true` to enable).
- **`run_stoPET`** *(Boolean)* – Whether to run the stoPET simulation (`true` to enable).
- **`run_DRYP`** *(Boolean)* – Whether to run the DRYP simulation (`true` to enable`).
- **`run_WaterCast`** *(Boolean)* – Whether to run the WaterCast simulation (`true` to enable).
- **`sim_in_parallel`** *(Boolean)* – If `false`, all processes run sequentially. If `true`, processes run in parallel (only for DRYP and impact map plotting).

---

### **Historical Data Parameters**
- **`model_name`** *(String)* – The name of the historical model.
- **`main_path`** *(String)* – Path to the main directory of the historical dataset.
- **`model_path`** *(String)* – Path to the directory containing historical model outputs.
- **`postpp_path`** *(String)* – Path to post-processed historical simulation outputs.

---

### **Forecasting Parameters**
- **`forecasting_model_name`** *(String)* – The name of the forecasting model.
- **`Tercile_Pre_path`** *(String)* – Path to the precipitation tercile NetCDF file (for StoPET).
- **`Tercile_Tem_path`** *(String)* – Path to the temperature tercile NetCDF file (for STORM).
- **`threshold_path`** *(String)* – Path to the threshold NetCDF data.
- **`season`** *(List of Strings)* – Season(s) for the simulation (e.g., `["OND"]`).
- **`start_year`** *(Integer)* – First year in the simulation period.
- **`end_year`** *(Integer)* – Last year in the simulation period.
- **`year`** *(Integer)* – The specific year for which the simulation is run.
- **`NSIM`** *(Integer)* – Number of simulation realizations.

---

## **MODEL-SPECIFIC INPUT FILES**

### **DRYP**
- **`input`** *(String)* – Path to the DRYP model input JSON.  
  See details [here](#dryp_parameters).  
- **`settings`** *(String)* – Path to the DRYP settings directory.  
  See details [here](#dryp_settings_parameters).

---

### **STORM**
- **`input`** *(String)* – Path to the STORM model input JSON.  
  See details [here](#storm_parameters).

---

### **stoPET**
- **`input`** *(String)* – Path to the stoPET model input JSON.  
  See details [here](#stopet_parameters).

---

### **WaterCast**
- **`HyCast`** *(String)* – Path to the **hydrological forecast input JSON** for HyCast.
- **`ImCast`** *(String)* – Path to the **impact forecast input JSON** for ImCast.


