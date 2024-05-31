---
title: "Software Packaging"
teaching: 10
exercises: 2
editor_options: 
  markdown: 
    wrap: 100
---


:::::::::::::::::::::::::::::::::::::: questions

- What is software packaging?
- How is packaging related to reproducibility and the FAIR4RS principles?
- What does packaging a python project look like?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Recognise the importance of software packaging to ensure  reproducibility.
- Understand what are the basic building blocks of a Python package.

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

One of the most challenging aspects of research is reproducibility. This necessitates the need to ensure that both research data and research software adhere to a set of guidelines that better enable open research practices across all disciplines. The recent adaptation of the original **FAIR** principles (Findable, Accessible, Interoperable, Reusable) means that research software can now also benefit from the same general framework as research data, whilst accounting for their inherent differences, including software versioning, dependency management, writing documentation, and choosing an appropriate license.


::::::::::::::::::::::::::::::::::::: discussion

Can you recall a time when you have used someone else's software but encountered difficulties in reproducing their results? What challenges did you face and how did you overcome them?

::::::::::::::::::::::::::::::::::::::::::::::::

Software packaging is one of the core elements of reproducible research software. In general, `software packaging` encompasses the process of collecting and configuring software components into a format that can be easily deployed on different computing environments.

<figure style="text-align: center;">
    <img src="fig/package.png" alt="alt text for accessibility purposes" width="300"/>
    <figcaption><em>A software package is like a box containing all the items you need for a particular activity, neatly packed together to transport to someone else</em>.</figcaption>
</figure>

::::::::::::::::::::::::::::::::::::: callout

Think about what a `package` is in general; you typically have a box of items that you want to post to someone else in the world. But before you post it for others to use, you need to make sure the package has things like: an address label, an instruction manual, and protective material.

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge

## Challenge 1: Packaging Analogy

Using the analogy in the callout above, provide an example for each package attribute in terms of the software attribute.


:::::::::::::::::::::::: solution

## Solution

1. Box of items: The software itself (source code, data, images).

2. Address label: Installation instructions specifying the target system requirements (operating system, hardware compatibility).

3. Instruction manual: User documentation explaining how to use the software effectively.

4. Protective materials: Error handling routines, data validation checks to safeguard the software from misuse or unexpected situations.

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::



## Overview of Software Packaging

The purpose of a software package is to install (or deploy) some source code in different systems that can be executed by other users. This has important considerations that you, as the developer, will have to take into account, including:

1. **Target Users**: Who are you building this package for? Beginners, experienced users, or a specific domain? This will influence the level of detail needed in the documentation and the complexity of dependencies you include.

2. **Dependencies**: What other Python libraries does your package rely on to function? What about hardware dependencies? Finding the right balance between including everything a user may need and keeping the package lightweight is important.

3. **Testability**: How will users test your package? Consider including unit tests and examples to demonstrate usage and ensure your code functions as expected.

Once you have thought about candidate solutions for these questions, you will be in a strong position to package your project.

### Packaging in Python

The most basic directory structure of a Python package looks something like:

```
📦 my_project/
├── 📂 my_package/
│   └── 📄 __init__.py
└── 📄 pyproject.toml

where

- 📦 `my_project/` is the root directory of the project.
- 📂 `my_package/` is the package directory containing the source code.
- 📄 `__init__.py` is an initialisation script (note; this also lets Python know that there are importable modules in this directory).
- 📄 `pyproject.toml` is a configuation file for setting up the package, containing basic metadata. Tools such as `setuptools` and `pip` use this script to configure how the package is built, distributed, and installed.
```


::::::::::::::::::::::::::::::::::::: callout

For example, consider the times you have imported a library, such as [numpy](www.numpy.org). The ability to write:

```python
import numpy
```
is primarily enabled by the specific (modular) structuring of the numpy package. This includes presence of the `__init__.py` file, which signals to Python that the directory is a package, allowing to import its content using the `import` statement. The complete `import numpy` statement then means Python searches for the `numpy` package  in its search path (`sys.path`) and loads its contents into the namespace under the name `numpy`.


::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: discussion

Another important point to highlight is the use of the ``__init__.py`` file in Python packages. In versions >= 3.3, Python introduced the concept of implicit namespace packages (see [PEP 420](https://peps.python.org/pep-0420/)). Namespace packages are a way of splitting a regular Python package (as described above) across multiple directories, which ultimately means the ``__init__.py`` file is not required to create a package. However, namespace packages are not commonly used, and it is common practise to still include ``__init__.py`` script to create "regular" packages. 

Apart from the reasons mentioned above, what other advantages can you think of that would enable software development best practises by including the ``__init__.py`` script? Can you find out which kind of projects benefit from namespace packages?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge

## Challenge 2: Improving your project's packaging

The directory structure of the basic Python package shown above is a good starting point, but it can be improved. From what you have learned so far, what other files and folders could you include in your package to provide better organisation, readability, and compatibility?



:::::::::::::::::::::::: solution

## Solution

A possible improvement could be to include the following to your package:

```
📦 my_project/
├── 📂 my_package/
│   └── 📄 __init__.py
├── 📂 tests/
├── 📄 pyproject.toml
├── 📄 README.md
└── 📄 LICENSE
```

The most obvious way to improve the package structure is to include a series of unit tests in a `tests` directory to demonstrate usage and ensure your code functions as expected. The main benefit of a `README.md` file is to provide essential information and guidance about a project to users, contributors, and maintainers in a concise and easily accessible format. Similarly, the purpose of a `LICENSE.md` file is to specify the licensing terms and conditions under which the package's code and associated assets are made available to others for use, modification, and distribution.

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

Although we have touched on the core concepts of packaging in Python, including how to set up one using the `pyproject.toml` configuration file, we still need to learn about how to write the metadata and logic for building a package. The next episode of this course provides a brief overview of the history of Python packaging, and what is required to turn your own project into a package.

::::::::::::::::::::::::::::::::::::: keypoints

- Reproducibility is an integral concept in the FAIR4RS principles. Appropriate software packaging is one way to account for reproducible research software, which involves collecting and configuring software components into a format deployable across different computer systems.

- Software packaging is akin to the packaging a box for shipment. Attributes such as the software source code, installation instructions, user documentation, and test scripts all support to ensure reproducibility.

- The purpose of a software package is to install source code for execution on various systems, with considerations including target users, dependencies, and testability.

::::::::::::::::::::::::::::::::::::::::::::::::

