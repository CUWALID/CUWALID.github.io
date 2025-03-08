## GitHub Installation

This package has been tested on **Windows, WSL on Windows, and Linux**. If you encounter issues a linux based system is recommended, if you are on windows please look into WSL 'Windows Subsystem for Linux'

Cloning the GitHub repository to use CUWALID allows greater control over the code.  
This installation method **uses Conda** to install Python and all dependencies.

If you **only need to run the model as it is**, the [PyPi package installation](#pypi_installation) may be simpler.

---

### **1. Clone the GitHub Repository**
First, open your terminal and **clone the repository**:

```bash
git clone https://github.com/CornishLeo/CUWALID.git
cd CUWALID
```

---

### **2. Set Up the Conda Environment**
Navigate to the **installers** directory and run the installation script:

```bash
cd installers

# For Windows:
cwld_wos.bat

# For Linux and WSL:
sh cwld_linux.sh
```

Wait for the installation to complete, then **activate your environment**:

```bash
conda activate cwld
```

Now, exit the **installers** directory and go back to the main CUWALID folder:

```bash
cd ..
```

---

### **3. Download Additional Data Files**
Some required files are too large to be stored on GitHub, so you need to download them separately.  

From the **root directory** of the project, run:

```bash
cd cuwalid/tools/
python download_data.py
```

---

### **4. Test the Installation**
Currently, testing is available for the **DRYP model**.

First, ensure your **Conda environment is activated**, then navigate to the **test directory** and run:

```bash
cd tests/dryp/
python run_tests.py
```

Once all the tests complete, the final output should look similar to this:

```bash
************************************************************
Infiltration approach: Philips
Run Interception component
100%|███████████████████████████████████████████████████████████████████████████████| 733/733 [00:21<00:00, 34.04days/s]
*** SAVING RESULTS ***
Traceback (most recent call last):
  File "/home/<username>/CUWALID/tests/test_dryp.py", line 24, in <module>
    test_dryp()
  File "/home/<username>/CUWALID/tests/test_dryp.py", line 19, in test_dryp
    assert np.allclose(out, ans)
AssertionError
Basin delineation: Test runs successfully
```

If the tests **start running**, the installation was successful! You can stop them early if needed.

---

### **5. Learn How to Run CUWALID**
You can learn how to run the model using the **[CUWALID Example GitHub Repository](https://github.com/CornishLeo/CUWALID-Example)**  
or by checking the [tutorial](#tutorial).
