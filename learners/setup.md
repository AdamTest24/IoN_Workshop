---
title: Setup
---

:::::::::::::::::: prereq
Before attempting today's sessions, you will need to have installed the following:

- Python 3.9
- conda
- pip3

:::::::::::::::::: 

## Data Sets

Download the [data zip file](data_files.zip) and unzip it to your Desktop.

## Software Setup

::::::::::::::::::::::::::::::::::::::: discussion

### Details
:::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::: solution

### Windows

Use PuTTY

:::::::::::::::::::::::::

:::::::::::::::: solution

### MacOS

Use Terminal.app

:::::::::::::::::::::::::


:::::::::::::::: solution

### Linux

Use Terminal

:::::::::::::::::::::::::


## Setting up virtual environment

Once you have Python/anaconda distribution installation. The packages can be installed bycreating an a Python environment.

<p style='text-align: justify;'>
In Python, the use of virtual environments allows you to avoid installing Python packages globally, which could disrupt system tools, or other projects.  Each virtual environment has its own Python binary (which matches the version of the binary that was used to create this environment), and can have its own independent set of installed Python packages within its site directories.
</p>


1. A virtual environment can be created by executing the following command in your Terminal (Mac OS and Unix), or on the command line prompt (Windows):

```
conda create -n ion_workshop python=3.9 pip
```

By running this command a new environment will be installed within your home directory.

2. The environment can be activated as:

```
conda activate ion_workshop 
```
3. In order to install the packages in your environment, write these commands on your terminal.

```
pip install numpy, matplotlib, pandas, scipy

pip install networkx==2.8.8

conda install -c conda-forge nibabel
```

4. At this point, everything will have been installed in our new environment. This is now the time to add this environment in your Jupyter Notebook, which can be done as follows:

```
conda install -c anaconda ipykernel
python -m ipykernel install --user --name=ion_workshop
```
<p style='text-align: justify;'>
After running these 2 commands, you will be able to select your virtual environment from the `Kernel` tab of your Jupyter notebook. More information can be accessed at this [link](https://medium.com/@nrk25693/how-to-add-your-conda-environment-to-your-jupyter-notebook-in-just-4-steps-abeab8b8d084).
</p>