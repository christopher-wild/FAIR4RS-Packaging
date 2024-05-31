---
title: "Versioning"
teaching: 10
exercises: 2
editor_options: 
  markdown: 
    wrap: 100
---


:::::::::::::::::::::::::::::::::::::: questions

- Why is versioning essential in software development? What problems can arise if versioning is not properly managed?
- How can automation tools, such as those for version bumping, improve the software development process?
- Why is it important to maintain consistency and transparency in software releases?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

-  Explain why versioning is crucial for software development, particularly in maintaining reproducibility and ensuring consistent behaviour of the code after changes.
- Understand how to use tools like Poetry and Python Semantic Release for automating the version bumping process in Python projects.
- Be able to create and integrate custom scripts or CI/CD pipelines for automated version bumping based on commit messages and predefined rules.

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

In previous episodes, we developed a basic Python package to demonstrate the importance of software reproducibility. However, a crucial question that we haven't addressed yet is: _how can we, as the developers, ensure that a change in our package's source code does not result in the code failing or behaving incorrectly?_ This is also an important consideration for when you are releasing your package.

::::::::::::::::::::::::::::::::::::: discussion

One of the pitfalls of packaging is to fall into poor naming conventions, even for scripts. For instance, how many times have you worked on scripts that was named `my_script_v1.py` or `my_script_final_version.py`? What were your main challenges with this approach, and what alternative solutions can you think of to circumvent this naive approach?

::::::::::::::::::::::::::::::::::::::::::::::::

## Semantic Versioning

<figure style="text-align: center;">
    <img src="fig/SemanticVersioning.png" alt="alt text for accessibility purposes" width="600"/>
    <figcaption><em>The framework of semantic versioning is described by three version numbers, major, minor and patch</em>.</figcaption>
</figure>


The answer the question above is based on a concept called `versioning`. Versioning is the practice of assigning unique version numbers to different states or releases of a given package to track its development, improvements, and bug fixes over time. The most popular approach for Python packaging is to use the [Semantic Versioning](https://semver.org/) framework, and can be summarised as follows:

```
Given a version number X.Y.Z, where X is the major version, Y is the minor version and Z is the patch version, you increment:

X when you make incompatible API changes,

Y when you add functionality in a backwards compatible manner,

Z when you make backwards compatible bug fixes. 


```

::::::::::::::::::::::::::::::::::::: callout

# API

An Application Programming Interface (API) is the name given to the way different programs or parts of a program to communicate with each other. It provides a set of functions, methods that can be used to interact with a piece of software or data services. Commonly, APIs are used within web-based applications to enable users to receive information from a given service, such as logging into social media accounts, creating weather widgets, or finding geographical locations. 

::::::::::::::::::::::::::::::::::::::::::::::::

The first version of any package typically starts at 0.1.0, and any changes following the semantic versioning rules above results in an increment to the appropriate version numbers. For example, updating a software from version (0.1.0) to (**1**.0.0) is called a `major` release. Version (**1**.0.0) is commonly referred to as the `first stable release` of the package.


An important point to highlight is the semantic versioning guidance above is a general rule of thumb. Exactly when you decide to bump the versions of your package is dependent on you, as the developer, to be able to make that decision. Developers typically take the size of the project into account as a factor; for example, small packages may require a patch release for every individual bug that is fixed. On the other hand, larger packages often group multiple bug fixes into a single patch release to help with tractability because making a release for every fix would accumulate in a myriad of releases, which can be confusing for users and other developers. The table below shows 3 examples of major, minor and patch releases developers made for Python. 


| Release Type  | Version Change | Description                                          |
|------------------------|-------------------------|--------------------------------------------------------------------------------|
| Major Release | 2.0.0 to 3.0.0 | Introduced significant and incompatible changes, such as the print function and new syntax.  |
| Minor Release | 3.7.0 to 3.8.0 | Added new features like the walrus operator and positional-only parameters, backward-compatible. |
| Patch Release | 3.8.0 to 3.8.1 | Fixed bugs and made performance improvements without adding new features or breaking changes. |

<figure style="text-align: center;">
    <figcaption><em>Table 1: Examples of major, minor and patch releases of Python</em>.</figcaption>
</figure>

::::::::::::::::::::::::::::::::::::: callout

# Pre-release Versions

Pre-release versions in semantic versioning are versions of the software that are still in development or testing before a stable release. They are denoted by appending a hyphen and a series of dot-separated identifiers to the version number, such as 1.0.0-alpha or 1.0.0-beta.1. These versions allow developers to release early versions for testing and feedback while clearly indicating their status.

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: callout

Once we publicly release a version of our software, it is crucial to maintain consistency and avoid altering it retroactively. Any necessary fixes needs to be addressed through subsequent releases, typically indicated by an increment in the patch number. 
For instance, Python 2 reached its final version, 2.7.18, in 2020, more than a decade after the release of Python 3.0. If the developers decided to discontinue support for an older version, leaving vulnerabilities unresolved, they would have to transparently communicate this to their users and encourage them to upgrade.

::::::::::::::::::::::::::::::::::::::::::::::::


::::::::::::::::::::::::::::::::::::: challenge

## Challenge 1: Semantic Versioning Decision Making

Imagine you are a developer working on a Python library called `DataTools`, which provides various utilities for data manipulation. The library uses semantic versioning and is currently at version 1.2.3. You have implemented a new feature that adds support for reading and writing CSV files with custom delimiters.

According to semantic versioning, should you bump the version to `1.3.0`, `1.2.4`, or `2.0.0`? Explain your reasoning.

:::::::::::::::::::::::: hint

## Hint

Think about whether the new feature introduces any breaking changes for existing users.

:::::::::::::::::::::::::::::::::

:::::::::::::::::::::::: solution

## Solution

According to semantic versioning, since the new feature adds functionality in a backward-compatible manner, the version should be bumped to `1.3.0`. This signifies a minor version increase.

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

## Tools for Version Bumping

At this point, you might be thinking; "__Do I have to manually update the version number in of my package every time I release a new version?__" Thankfully, the answer is no. Often, the version number associated to your package will typically be in multiple locations within your project, for example, in your `.toml` file and separately in your documentation. This means that manually updating every location for every release you have can be extremely cumbersome and prone to human-error, and therefore, you should avoid manually updating your versions. There are several tools that can help you manage updating your package versions.


### 1. Poetry

[Poetry](https://python-poetry.org/) is a dependency management and packaging tool for Python projects. It aims to simplify the process of managing dependencies, packaging projects, and publishing them to online repositories. For this, you will have to decide what release type (major, minor patch) reflects the changes in your source code. For projects that are managed by Poetry, the version number is in your `pyproject.toml` file. For instance, your `pyproject.toml` file may look like:

```toml

[tool.poetry]
name = "my_project"
version = "0.1.0"
description = "A simple example project"
authors = ["Your Name"]

```
Once you have decided on the type of release (e.g. patch), you can simply run:

```bash
$ poetry version patch

```

This bumps the version in your toml file from 0.1.0 to 0.1.1, and changes your `.toml` file to:

```toml

[tool.poetry]
name = "my_project"
version = "0.1.1"
description = "A simple example project"
authors = ["Your Name"]

```

::::::::::::::::::::::::::::::::::::: callout

Like a `venv`, Poetry also enables creating virtual environments, but it provides a more comprehensive toolset for dependency and environment management, especially when it comes to packaging and reproducibility. For instance, Poetry's `poetry.lock` file ensures that exact versions of dependencies are used across different environments. This is one way research software reproducibility can be maintained. 

::::::::::::::::::::::::::::::::::::::::::::::::

### 2. Python Semantic Release

[Python Semantic Release](https://python-semantic-release.readthedocs.io/en/latest/) is a tool that can automatically bump versions based on keywords found in commit messages using Git. The core idea is to use a standardised commit syntax that allows the tool to parse and automatically determine how to increment the version number. The default commit syntax used by Python Semantic Release is the Angular commit style, which has the following form:

```
<type>(optional scope): brief overview in present tense

(optional body: explains motivation for the change)

(optional footer: note BREAKING CHANGES here, and issues to be closed)

```

The tag ``<type>`` highlights the kind of change that is being made. Examples of this include ``feat`` for a new feature, ``fix`` for a bug fix, ``docs`` for documentation changes and so on. For more information, please refer to the Angular commit style [documentation](https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#commit-message-format).

The ``(optional scope)`` is a keyword that provides additional context for where the change was made in your code base. It can relate to any information in your development workflow, such as the function or module that was changed.

Putting this together, once you have git added your file(s), a commit message that would trigger Python Semantic Release to bump your package from version 1.1 to version 1.2 due to a new feature could look something like:

```bash
$ git commit -m "feat(add_estimator): add estimator method for linear regression"

```

Once you have committed, you can run ``$ semantic-release version`` in your terminal to detect the semantically correct next version that should be applied to your project,  or  ``$ semantic-release publish`` to publish to your choice of version control system (e.g. GitHub).

### 3. Creating your own Versioning Tool

You can also create your own custom version bump tool using continuous integration (CI) / continuous deployment (CD) pipelines on various version control systems (such as GitHub) to automate your package's versioning.  For instance, you might develop a custom script that is executed to analyse commit messages, and whenever a push is made to the remote repository, the CI/CD pipeline is triggered. The script can parse the commit messages and determines the type of changes made (e.g., new features, bug fixes, maintenance tasks). Based on predefined rules, it decides whether to increment the major, minor, or patch version. Once the script determines the appropriate version bump (major, minor, or patch), you can specify where to update the version number in the project's configuration files (e.g. `pyproject.toml`, `/docs`, `/tests`, and so on.). After updating the version number, the script would create a new commit with the updated version number. Ultimately, the script tags the commit as the new release version. This tag can be used for referencing specific releases in the future.


::::::::::::::::::::::::::::::::::::: callout

As a reminder, Continuous Integration/Continuous Deployment is a software development practice that involves automating the process of integrating code changes into a shared repository (CI) and then automatically deploying those changes to production or other environments (CD). GitHub Actions is a common example of a CI/CD tool, which allow developers to seamlessly automate workflows directly within their GitHub repositories.

::::::::::::::::::::::::::::::::::::::::::::::::



::::::::::::::::::::::::::::::::::::: challenge

## Challenge 2: Version Bumping your Package

Following the instructions above, install `Poetry` and use this to update your Fibonacci package you have build based on the changes you have made to your code.


:::::::::::::::::::::::: solution

## Solution

Simply run:

1. ``$ pip install poetry``
2. Make changes to your code
3. Run ``$ poetry version minor`` to change the minor version number to reflect the changes in your code.

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::


::::::::::::::::::::::::::::::::::::: keypoints

- Versioning is crucial for tracking the development, improvements, and bug fixes of a software package over time. It ensures that changes are documented and managed systematically, aiding in reproducibility and reliability of the software.

- Tools like Poetry and Python Semantic Release help automate the version bumping process, reducing manual errors and ensuring that version numbers are updated consistently across all project files.

- Once a version is publicly released, it should not be altered retroactively. Any necessary fixes should be addressed through subsequent releases.

::::::::::::::::::::::::::::::::::::::::::::::::

