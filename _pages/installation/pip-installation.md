---
title: "Pip Installation"
layout: single
permalink: /tutorials/pip-installation

sidebar:
  nav: "tutorials"

---

These steps assume you already have Anaconda installed to easily create new environments. We recommend using a **Python version between 3.9 and 3.11**. If you aren't using anaconda, it is still recommended to create an environment.

If you don't have Anaconda or Python installed yet, check out the instructions [here](#python-tutorial).  
Make sure to **tick the "Add to PATH" box** during installation to simplify the setup.

---

### **1. Create a Virtual Environment (Recommended)**
First, open the directory where you want to work and ensure Python or Anaconda is properly installed.  
It is recommended to create a **virtual environment** before installation.  

If using Conda, run:

```bash
# Create a Conda environment named "test_env" with Python 3.11
conda create --name test_env python=3.11 -y
conda activate test_env
```

Now your environment is created and activated.

---

### **2. Install CUWALID Package**
Run the following command to install the latest version of CUWALID:  

```bash
# This is currently only on the test version of PyPI and will need to be updated when fully released
pip install -i https://test.pypi.org/simple/ --extra-index-url https://pypi.org/simple CUWALID
```

This will install CUWALID along with all required dependencies.

#### **Updating CUWALID**
To update CUWALID to the newest version, run:

```bash
pip install -i https://test.pypi.org/simple/ --extra-index-url https://pypi.org/simple CUWALID --upgrade
```

#### **Installing GDAL for Storm**
If you are using **Storm**, you will also need **GDAL**.  
The easiest way to install it is via Conda (instead of pip):

```bash
conda install gdal "numpy<2.0"  # Ensure correct compatibility with Storm
```

---

### **3. Run Tests (Optional)**
You can run tests to verify that CUWALID was installed correctly.  

If the tests start running, you can **stop them early**—this confirms a successful installation.

```bash
python -m cuwalid.tests.dryp.run_tests
python -m cuwalid.tests.stopet.run_tests
```

---

### **4. Running CUWALID**
To run the full CUWALID system, check out the tutorial [here](/tutorials/#cuwalid).  
You can also use the [CUWALID Example GitHub Repository](https://github.com/AndresQuichimbo/CUWALID-Example) to access example input files.


