---
title: "Python Tutorial"
layout: single
permalink: /tutorials/python-tutorial

sidebar:
  nav: "tutorials"

---

This section provides recommendations for learning Python, especially if you're new to coding. The tutorials listed here are **not affiliated** with the CUWALID Team but are **free online resources** we highly recommend.  

### Downloading Python

The easiest way to start with Python is by using **Anaconda**, a platform that simplifies installation, environment management, and package dependencies (which is essential for CUWALID). We **strongly recommend** using Anaconda to create environments with specific python versions and using `pip` to install dependencies as described [here](/tutorials/#pip-installation).  

<a href="https://www.anaconda.com/download" class="btn btn--primary" target="_blank">Download Anaconda here</a>

Alternatively, you can download Python directly from the official website:  

<a href="https://www.python.org/downloads/release/python-3110/" class="btn btn--primary" target="_blank">Download Python 3.11</a>

### Python Help

Python is an excellent language for beginners—it's **easy to learn**, widely used, and has countless **free resources** available online. Below are some recommended tutorials (not affiliated with CUWALID):  

- **[Official Python Tutorial](https://docs.python.org/3/tutorial/)** – In-depth, covers every core feature of Python.  
- **[W3Schools Python Tutorial](https://www.w3schools.com/python/)** – A beginner-friendly resource with interactive examples.  
- **[FreeCodeCamp Python Course](https://www.youtube.com/watch?v=rfscVS0vtbw)** – A great **YouTube** tutorial for absolute beginners (shown below).  

{% include video id="rfscVS0vtbw" provider="youtube" %}



### Python basics for CUWALID users

CUWALID uses well-known packages to handle information and perform calculations. You will find the following packages useful for preparing model parameters as well as analyzing model outputs. Here, you will also find links to widely used, **free resources** available online (not affiliated with CUWALID):


- **[Handling time series with pandas](https://pandas.pydata.org/docs/getting_started/intro_tutorials/09_timeseries.html)** – Pandas is a very powerful package for managing all kinds of tabular data, including time series (e.g., *.csv). The latter is one of the common CUWALID output formats. In this link, you will find instructions on how to create and manage time series and tabular datasets.

- **[Create netCDF files with xarray](https://docs.xarray.dev/en/latest/user-guide/data-structures.html)** – Here, you will find information on how to create, open, and process netCDF files, one of the most common formats used in climatological sciences and widely used in CUWALID. 

- **[Visualising model ouputs with xarray](https://docs.xarray.dev/en/latest/user-guide/plotting.html)** – Plotting netCDF datasets, a common gridded dataset format for CUWALID outputs. 

- **[Handling raster dataset with rasterio](https://rasterio.readthedocs.io/en/stable/topics/reading.html)** – You can use rasterio to create raster files (e.g., *.ASC, *.tif), which are common gridded formats for CUWALID model parameters.


### CUWALID Python Training

This training package provides a series of hands-on Python tutorials designed to support users in creating, managing, and working with CUWALID datasets. The tutorials are delivered as Jupyter Notebooks and cover essential data preparation tasks for hydrological and environmental modeling workflows using CUWALID.

Whether you are working with time series or spatial data, these tutorials will guide you through key operations needed to build and customize your own datasets.

All **Jupyter Notebooks** for Python tutorial are found here:

<a href="https://github.com/AndresQuichimbo/CUWALID-tutorials/tree/main/Training/Python" target="_blank" class="btn btn--primary">
    <img src="/assets/images/icons/github-mark.svg" alt="GitHub" class="icon"> Python Tutorial
</a>


#### Training modules
1. **[Creating 1D and 2D Temporal Series in Python](https://github.com/AndresQuichimbo/CUWALID-tutorials/blob/main/Training/Python/Timeseries_generator.ipynb)**
Learn how to generate and manage temporal datasets in Python, including both single-point (1D) and spatially distributed (2D) time series that are compatible with CUWALID workflows.

2. **[Creating Raster Files in Python](https://github.com/AndresQuichimbo/CUWALID-tutorials/blob/main/Training/Python/Create_raster_files_samples.ipynb)**
This tutorial walks through the process of creating raster datasets from scratch using Python. You'll learn how to define grid structures, assign values, and save outputs in standard raster formats.

3. **[Modifying Raster Files Using Region-Based Values](https://github.com/AndresQuichimbo/CUWALID-tutorials/blob/main/Training/Python/Create_raster_datasets_from_table.ipynb)**
Learn how to update existing raster datasets using a list of predefined regions and corresponding values. This approach is useful for tasks such as assigning land use categories, parameter zones, or scenario-based modifications.



