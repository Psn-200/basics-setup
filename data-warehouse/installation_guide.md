# Setting up Python with Conda on Windows: A Student's Guide

As a student, getting your Python environment set up correctly on Windows is the crucial first step. This guide will walk you through choosing a Conda distribution, installing it properly, configuring it for your terminal, and using it in your notebooks.

---

## 1. Anaconda vs. Miniconda: Which should I choose?

- **Miniconda (Highly Recommended):** A lightweight, minimal installer. It includes only Conda, Python, and a few essential packages. You only download what you need, saving significant disk space and keeping your system clean.
- **Anaconda:** A massive distribution that comes pre-packaged with a GUI (Anaconda Navigator) and over 1,500 data science packages (NumPy, Pandas, Matplotlib, etc.). Choose this only if you have plenty of storage space and prefer a "batteries-included" approach without manual installations.

> [!TIP]
> **Start with Miniconda**. You can always install any package you need later using `conda install <package_name>`.

---

## 2. Downloading and Installing

1. Download the **Windows 64-bit installer**:
   - [Miniconda Downloads](https://docs.conda.io/en/latest/miniconda.html)
   - [Anaconda Downloads](https://www.anaconda.com/download)
2. Run the downloaded `.exe` installer.
3. Click "Next" through the prompts until you reach the **Advanced Installation Options**.
4. **Crucial Step:** 
   - **Do NOT check** "Add Anaconda/Miniconda to my PATH environment variable". *(The installer warns against this because it can cause conflicts with other software. We will set it up properly in the next step).*
   - **Check** "Register Anaconda/Miniconda as my default Python 3.x".
5. Click **Install** and wait for it to finish.

---

## 3. Adding Conda to Your Environment (PowerShell)

Instead of manually editing the messy Windows `PATH` variables, the safest and officially recommended way to use Conda is to "initialize" it for your shell.

1. Open the Windows Start Menu, search for **Anaconda Prompt** (or **Miniconda Prompt**), and open it. *(This special prompt already knows where Conda lives).*
2. Inside this prompt, run the following command to link Conda to your standard Windows PowerShell:
   ```powershell
   conda init powershell
   ```
3. **Windows Security Fix:** By default, Windows PowerShell blocks scripts from running, which will prevent Conda from activating. To fix this:
   - Right-click your Start Menu, select **Windows PowerShell (Admin)** or **Terminal (Admin)**.
   - Run this exact command:
     ```powershell
     Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
     ```
   - Type `Y` and press Enter when prompted.
4. **Restart your terminals.** Close all open terminal windows or restart VS Code. When you open a new PowerShell terminal, you should now see `(base)` at the very beginning of the prompt line. This means Conda is active and ready!

> [!NOTE] 
> If you strictly require Conda in your raw Windows System `PATH` (sometimes needed for older tools), you must manually add these three folders to your User Environment Variables (assuming a default installation):
> - `C:\Users\<YourUsername>\miniconda3`
> - `C:\Users\<YourUsername>\miniconda3\Scripts`
> - `C:\Users\<YourUsername>\miniconda3\Library\bin`

---

## 4. Creating Environments & Selecting the Kernel

Never install project packages directly into your `(base)` environment. Always create a dedicated environment for your project.

### Step A: Create and prepare the environment
Open your PowerShell terminal and run:
```powershell
# 1. Create an environment named 'myenv' with a specific Python version
conda create --name myenv python=3.10 -y

# 2. Activate the new environment (your prompt will change from base to myenv)
conda activate myenv

# 3. Install the Jupyter kernel package so VS Code can see this environment
conda install ipykernel -y
```

### Step B: Use it in VS Code / Jupyter Notebooks
1. Open your project folder in VS Code and open your `.ipynb` notebook file.
2. Look at the top right corner of the notebook interface. You will see a button to **Select Kernel** (it might currently say "Python", "base", or "Detecting Kernels...").
3. Click it and choose **Python Environments** (or "Jupyter Kernel").
4. Select the environment you just created (`myenv`).
   
> [!TIP]
> If you don't see `myenv` in the list immediately, click the refresh icon `↻` in the dropdown menu, or simply close and reopen VS Code.

---

## 5. Managing Packages

Once your environment is activated, you can install packages and check what is installed.

### Installing Packages

You can use `pip` or `conda` to install packages. For example, to install `pandas` and `numpy`:

```powershell
# Using pip (often has the latest versions)
pip install pandas numpy

# Or using conda
conda install pandas numpy -y
```

### Checking Installed Packages and Versions (Terminal)

To see a list of all packages installed in your active Conda environment, run:

```powershell
conda list
```

To check the version of a specific package (e.g., pandas), you can use:

```powershell
pip show pandas
```

### Checking Versions in Jupyter Notebooks

You can also verify package versions directly within your notebook to ensure your code is using the right environment.

**Using Python:**
```python
import pandas as pd
import numpy as np

print(f"Pandas version: {pd.__version__}")
print(f"NumPy version: {np.__version__}")
```

**Using Shell Commands in Notebooks:**
You can run terminal commands inside a notebook cell by adding an exclamation mark `!` at the beginning:
```python
!conda list
!pip show pandas
```
