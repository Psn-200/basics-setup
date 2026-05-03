# Conda Environment and Package Management Guide

This guide covers essential Conda commands and concepts for creating, managing, and maintaining isolated Python environments.

## 1. Creating Environments

Creating isolated environments is a core feature of Conda. It allows you to maintain different versions of packages and Python itself for different projects.

* **Create a new environment with a specific Python version:**
  ```bash
  conda create --name myenv python=3.10
  ```
  *(Replace `myenv` with your desired environment name)*

* **Create an environment and install specific packages immediately:**
  ```bash
  conda create --name myenv python=3.9 pandas numpy scikit-learn
  ```

* **Create an environment from an `environment.yml` file (Best Practice for Reproducibility):**
  ```bash
  conda env create -f environment.yml
  ```

* **Clone an existing environment:**
  ```bash
  conda create --name myclone --clone myenv
  ```

## 2. Activating and Deactivating Environments

Before using the packages in an environment, you must activate it.

* **Activate an environment:**
  ```bash
  conda activate myenv
  ```

* **Deactivate the current environment (returns to the `base` environment):**
  ```bash
  conda deactivate
  ```

## 3. Viewing and Listing Environments & Packages

* **List all created Conda environments:**
  ```bash
  conda env list
  ```
  *or*
  ```bash
  conda info --envs
  ```

* **List all packages installed in the *active* environment:**
  ```bash
  conda list
  ```

* **List all packages installed in a *specific* environment (without activating it):**
  ```bash
  conda list -n myenv
  ```

* **Search for a specific package in the active environment:**
  ```bash
  conda list <package_name>
  ```

## 4. Installing and Updating Packages

* **Install a package:**
  ```bash
  conda install <package_name>
  ```

* **Install a specific version of a package:**
  ```bash
  conda install <package_name>=1.2.3
  ```

* **Install a package from a specific channel (e.g., `conda-forge`):**
  ```bash
  conda install -c conda-forge <package_name>
  ```

* **Update a specific package:**
  ```bash
  conda update <package_name>
  ```

* **Update all packages in the active environment:**
  ```bash
  conda update --all
  ```

## 5. Deleting Environments and Packages

* **Remove a specific package from the active environment:**
  ```bash
  conda remove <package_name>
  ```

* **Delete an entire environment and all its packages:**
  ```bash
  conda env remove --name myenv
  ```

* **Clean up unused packages and caches (free up disk space):**
  ```bash
  conda clean --all
  ```

## 6. Multiple Versioning & Best Practices

Managing different versions of packages is crucial for project stability.

* **Pinning Versions:** When creating environments or sharing them, always specify exact package versions to avoid future conflicts.
* **Exporting Environments:** To share your setup with others or for deployment, export your environment configuration:
  ```bash
  conda env export > environment.yml
  ```
* **Using `environment.yml`:** This file defines the exact dependencies (including versions) required for your project. A typical `environment.yml` looks like this:
  ```yaml
  name: myproject_env
  channels:
    - defaults
    - conda-forge
  dependencies:
    - python=3.10
    - numpy=1.24.3
    - pandas=2.0.1
    - pip:
      - some-pypi-only-package==1.0.0
  ```
* **Why use Conda?** Conda handles non-Python dependencies (like C libraries) much better than `pip` alone, which is especially useful for data science and machine learning projects.

## 7. Using Conda Environments in Jupyter Notebooks / VS Code

To ensure your newly created environment is visible in Jupyter Notebooks or as a kernel in VS Code:

1. **Activate your environment:**
   ```bash
   conda activate myenv
   ```
2. **Install `ipykernel`:**
   ```bash
   conda install ipykernel
   ```
3. **Add the environment as a Jupyter kernel:**
   ```bash
   python -m ipykernel install --user --name=myenv --display-name="Python (myenv)"
   ```
Now, when you open a Jupyter Notebook in VS Code, you can select "Python (myenv)" from the kernel dropdown.

---

# Python Virtual Environments (`venv`) Guide

While Conda is a powerful tool for managing environments (especially for data science), Python's built-in `venv` module is another extremely popular, lightweight way to create isolated Python environments. It comes pre-installed with Python 3.3+.

## 1. Creating Virtual Environments

* **Create a new virtual environment:**
  Navigate to your project directory and run:
  ```bash
  python -m venv myenv
  ```
  *(Replace `myenv` with your desired folder name. Common names are `.venv`, `venv`, or `env`.)*

## 2. Activating Virtual Environments

Activation changes your shell's `PATH` to use the environment's Python and `pip`. The command depends on your operating system.

* **On Windows (Command Prompt):**
  ```cmd
  myenv\Scripts\activate.bat
  ```

* **On Windows (PowerShell):**
  ```powershell
  myenv\Scripts\Activate.ps1
  ```

* **On macOS and Linux:**
  ```bash
  source myenv/bin/activate
  ```

Once activated, your command prompt will usually change to show the environment name (e.g., `(myenv) C:\Projects>`).

## 3. Deactivating Virtual Environments

* **Deactivate the current environment:**
  ```bash
  deactivate
  ```

## 4. Installing Packages

With `venv`, you use Python's default package manager, `pip`, to install dependencies.

* **Install a package:**
  ```bash
  pip install <package_name>
  ```

* **Install a specific version:**
  ```bash
  pip install <package_name>==1.2.3
  ```

* **Upgrade a package:**
  ```bash
  pip install --upgrade <package_name>
  ```

* **List installed packages:**
  ```bash
  pip list
  ```

## 5. Managing Dependencies (`requirements.txt`)

Instead of Conda's `environment.yml`, `venv` typically uses a `requirements.txt` file to track dependencies.

* **Export installed packages to a requirements file:**
  ```bash
  pip freeze > requirements.txt
  ```

* **Install packages from a requirements file:**
  ```bash
  pip install -r requirements.txt
  ```

## 6. Deleting Virtual Environments

Since a virtual environment is just a directory, deleting it is as simple as deleting the folder.

* **On Windows (Command Prompt / PowerShell):**
  ```cmd
  rmdir /s /q myenv
  ```

* **On macOS and Linux:**
  ```bash
  rm -rf myenv
  ```

## 7. Using `venv` in VS Code / Jupyter

To use a `venv` environment in your notebook:

1. **Activate your environment.**
2. **Install `ipykernel`:**
   ```bash
   pip install ipykernel
   ```
3. **Register the environment as a kernel:**
   ```bash
   python -m ipykernel install --user --name=myenv --display-name="Python (myenv-venv)"
   ```
Now it will be available as a kernel option in your VS Code notebooks.
