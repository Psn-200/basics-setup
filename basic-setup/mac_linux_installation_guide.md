# Setting up Python with Conda on macOS and Linux: A Student's Guide

As a student, getting your Python environment set up correctly is the crucial first step. This guide will walk you through choosing a Conda distribution, installing it on your Mac or Linux system, configuring it for your terminal, and using it in your notebooks.

---

## 1. Anaconda vs. Miniconda: Which should I choose?

- **Miniconda (Highly Recommended):** A lightweight, minimal installer. It includes only Conda, Python, and a few essential packages. You only download what you need, saving significant disk space and keeping your system clean.
- **Anaconda:** A massive distribution that comes pre-packaged with a GUI (Anaconda Navigator) and over 1,500 data science packages (NumPy, Pandas, Matplotlib, etc.). Choose this only if you have plenty of storage space and prefer a "batteries-included" approach without manual installations.

> [!TIP]
> **Start with Miniconda**. You can always install any package you need later using `conda install <package_name>`.

---

## 2. Downloading and Installing

### For macOS
1. Download the **macOS installer** (choose between Intel x86_64 or Apple Silicon ARM64 depending on your Mac):
   - [Miniconda Downloads](https://docs.conda.io/en/latest/miniconda.html)
2. You can either download the `.pkg` file and double-click to install it like a normal Mac application, OR download the `.sh` script and install it via the terminal:
   ```bash
   bash Miniconda3-latest-MacOSX-arm64.sh
   ```

### For Linux
1. Open your terminal and download the latest installer script using `wget` or `curl`:
   ```bash
   mkdir -p ~/miniconda3
   wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
   ```
2. Run the installation script:
   ```bash
   bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
   ```
3. Initialize conda for your shell (e.g., bash or zsh):
   ```bash
   ~/miniconda3/bin/conda init bash
   # or if you use zsh:
   ~/miniconda3/bin/conda init zsh
   ```

> [!NOTE]
> During a manual script installation (`.sh`), the installer will eventually ask: "Do you wish the installer to initialize Miniconda3 by running conda init?". **Type `yes` and press Enter.** This step is crucial!

---

## 3. Verifying the Installation

After installing, **close and reopen your terminal**. 

When you open a new terminal window, you should now see `(base)` at the very beginning of your prompt line. This means Conda is active and ready!

```bash
# Verify conda is working
conda --version
```

---

## 4. Creating Environments & Selecting the Kernel

Never install project packages directly into your `(base)` environment. Always create a dedicated environment for your project.

### Step A: Create and prepare the environment
Open your terminal and run:
```bash
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

```bash
# Using pip (often has the latest versions)
pip install pandas numpy

# Or using conda
conda install pandas numpy -y
```

### Checking Installed Packages and Versions (Terminal)

To see a list of all packages installed in your active Conda environment, run:

```bash
conda list
```

To check the version of a specific package (e.g., pandas), you can use:

```bash
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
