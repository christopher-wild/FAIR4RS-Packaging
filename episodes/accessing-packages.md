---
title: 'Accessing Packages'
teaching: 10
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions 

- What are the different ways of downloading python packages?
- What are package managers?
- How can I use my own package?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Learn about package managers such as PIP
- Install packages using PIP
- Install packages from source

::::::::::::::::::::::::::::::::::::::::::::::::


## Introduction

Due to Pythons popularity as a language, it is quite likely that you won't be the first person to set off on solving any particular task.
Many others have worked on common problems and then shared their solution in the form of a pacakge, which you can conveniently integrate into your own code and use!

::: callout

### Popular Packages
Some of the most popular packages you may have heard of are:

- Numpy
- Pandas
- Tensorlow
- Matplotlib
- Requests

:::

### Python Package Index (PyPI)

The Python Package Index or PyPI is an online repository of Python packages  hosting over 500,000 packages! While there are alternatives such as [conda-forge](https://conda-forge.org), PyPI is by far the most commonly used and likely to have all you need.


::: callout
### pip

pip (package installer for Python) is the standard tool for installing packages from PyPI. 
You can think of PyPI being the supermarket full of packages and pip being the delivery van bringing it to your installation.

:::


### Using pip

pip itself is a python package that can be found on [PyPI](https://pypi.org/project/pip/), however it comes preinstalled with most python installations, for example [python.org](https://python.org) and inside virtual environments.

The most common way to use pip is from the command line. At the top of a package page on PyPI will be the example line you need to install the package

::: spoiler

### Virtual Environments

Check out [this documentation](https://docs.python.org/3/l[PyPI](https://pypi.org/project/pip/)ibrary/venv.html) or the FAIR4RS course on virtual environments to learn more!

:::

::: challenge

### Exercise 1: Explore PyPI

Explore [PyPI](https://pypi.org/project/pip/) to get familiar with it, try searching for packages that are relevant to your research domain / role!

:::

