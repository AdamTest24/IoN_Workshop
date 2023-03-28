---
title: Setup
---

## Python 3
<p style='text-align: justify;'>
It is sometimes claimed that biologist should use Python 2, because most biology related libraries in Python are written for that version. This is wrong. The reason why Python 2 is still out there is that following the release of Python 3.0 in December 2008, the CPython interpreter sustained several problems, and was not backward compatible. This meant that, any code written in Python 2, could *not* be run using Python 3 without modifications. By now, Python 2 is obsolete. Do not use it.
</p>

## Why Anaconda?
<p style='text-align: justify;'>
For the purpose of this course, we recommend the Anaconda distribution of Python released by the [Python Software Foundation](https://www.python.org/psf-landing/), and maintained by the [Anaconda Cloud](https://anaconda.org/).
</p>

<p style='text-align: justify;'>	
Anaconda automatically installs many packages needed for scientific purposes (over 250 automatically installed). It is easy to install, and it takes care of dependencies between packages. This is particularly important because some of Python's scientific libraries require Fortran-- and C--based libraries, which may be challenging to install for beginners.
</p>

## Installation
<p style='text-align: justify;'>
To install the Anaconda distribution of Python, please visit the [installation instructions](https://docs.anaconda.com/anaconda/install/) as outlined in the Anaconda [documentations](https://docs.anaconda.com/anaconda/install/), and follow the instructions for your operating system. Ensure that you use the Python 3.x graphical installer for Windows and MacOSX (there is no graphical installer for Linux). Once downloaded, you can proceed to install the distribution as you would any other application on your computer.
</p>

<p style='text-align: justify;'>
Anaconda Navigator is a desktop graphical user interface (GUI) included in Anaconda distribution that allows users to launch applications and manage conda packages, environments and channels without using command-line commands. Navigator can search for packages on Anaconda Cloud or in a local Anaconda Repository, install them in an environment, run the packages and update them. It is available for Windows, macOS and Linux.
</p>

The following applications are available by default in Navigator:

 - JupyterLab
 
 - Jupyter Notebook
 
 - QtConsole
 
 - Spyder
 
 - Glue
 
 - Orange
 
 - RStudio
 
 - Visual Studio Code


We recommend using JupyterLab for writing and practicing your codes. 


### Starting with JupyterLab
Here is the video to learn using JupyterLab

<p align = "center">
<iframe width="560" height="315" src="https://www.youtube.com/embed/sem75rYIrvM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</p> 


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

pip install numpy, pandas, scipy, seaborn

pip install networkx==2.8.8

conda install matplotlib

conda install scikit-learn

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

## Data Sets

Download the [data zip file](data_files.zip) and unzip it to your Desktop.