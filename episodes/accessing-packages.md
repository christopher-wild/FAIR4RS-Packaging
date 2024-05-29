---
title: 'Accessing Packages'
teaching: 30
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions 

- What are the different ways of downloading python packages?
- What are package managers?
- How can I access my own package?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Learn about package managers such as PIP
- Install packages using PIP
- Install packages from source

::::::::::::::::::::::::::::::::::::::::::::::::


## Introduction

Due to Pythons popularity as a language, it is quite likely that you won't be the first person to set off on solving any particular task.
Many others have worked on common problems and then shared their solution in the form of a package, which you can conveniently integrate into your own code and use!

::: callout

### Popular Packages
Some of the most popular packages you may have heard of are:

- Numpy
- Pandas
- Tensorlow
- Matplotlib
- Requests

:::

To use a package that is installed you use the key word `import` in python.

```python
# This imports the pandas package and gives it a new name 'pd'.
import pandas as pd 

# Use the package to read a file
pd.read_csv("/my_data.csv") 
```

## Python Package Index (PyPI)

The Python Package Index or PyPI is an online repository of Python packages  hosting over 500,000 packages! While there are alternatives such as [conda-forge](https://conda-forge.org), PyPI is by far the most commonly used and likely to have all you need.

::: challenge

### Exercise 1: Explore PyPI

Explore [PyPI](https://pypi.org/project/pip/) to get familiar with it, try searching for packages that are relevant to your research domain / role!

:::

::: callout
### pip

pip (package installer for Python) is the standard tool for installing packages from PyPI. 
You can think of PyPI being the supermarket full of packages and pip being the delivery van bringing it to you.

:::


### Using pip

pip itself is a python package that can be found on [PyPI](https://pypi.org/project/pip/). It however comes preinstalled with most python installations, for example [python.org](https://python.org) and inside virtual environments.

The most common way to use pip is from the command line. At the top of a package page on PyPI will be the example line you need to install the package

```
py -m pip install numpy
```

The above will install [numpy](https://pypi.org/project/numpy/) from PyPI, a popular scientific computing package enabling a wide range of mathematical and scientific functions. 


::: challenge
### Exercise 2: Create venv and install Numpy

Step 1: Create a venv in the .venv directory using the command `py -m venv .venv` and activate it with

::: tab

### Windows 

`.\.venv\Scripts\activate`



### macOS / Linux

`source .venv/bin/activate`


:::

Step 2: Install Numpy into your new environment

Step 3: Check your results with `py -m pip list`

Step 4: Deactivate your environment with `deactivate`

:::

::: spoiler

### Virtual Environments

Check out [this documentation](https://docs.python.org/3/l[PyPI](https://pypi.org/project/pip/)ibrary/venv.html) or the FAIR4RS course on virtual environments to learn more!

:::


pip can also be used to install packages from source. This means that the package file structure (source) is on your local computer and pip installs it using the instructions from the `setup.py` or `pyproject.toml` file. This is especially handy for packages either not on PyPI, like ones downloaded from github, or for your own packages you're developing.

```
py -m pip install .
```

::: instructor

The above command should be universal on both windows and mac/unix setups. It may be worth checking with the class at this point that they are all familiar with the -m notation, and what the above command does exactly

:::

Here the `.` means to install your current directory as a Python package. For this to work the directory your command line interface is currently in needs to have a packaging file, i.e. `setup.py` or `pyproject.toml`. 



::: keypoints
- pip can be used to download and install Python packages
- PyPI is an online package repository which pip downloads from
- pip can also install local packages like your own
:::






