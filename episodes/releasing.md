---
title: "Publishing Packages"
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

Now that we have covered the fundamentals of packaging in Python, we can start preparing to publish the package online for others to use. But before we do, we need to make sure our package contains the necessary files. To recap, let's review the basic directory we created back in episode one, which had the following structure:


```
📦 my_project/
├── 📂 my_package/
│ └── 📄 init.py
├── 📂 tests/
├── 📂 docs/
│ └── 📄 documentation.md
├── 📄 pyproject.toml
├── 📄 README.md
└── 📄 LICENSE
```

### README 

Firstly, all packages must contain a `README.md` file that explains what the project is. how users can install it and how they can use it. A good example of a `README.md` file may look something like:

```

# My Python Project

My Python Project is a simple utility tool designed to perform basic operations on text files. Whether you need to count words, find specific phrases, or extract data, this tool has you covered.

## Installation

You can install My Python Project via pip:

$ pip install my-python-project

## Usage

from my_python_project import text_utils

text = "Lorem ipsum dolor sit amet, consectetur adipiscing elit."
word_count = text_utils.count_words(text)
print("Word count:", word_count)

This will output:

Word count: 9

```

Notice that the `README.md` should be included at the top level of our project directory. If your package was created using a `.toml` file, it should also be included in the metadata by adding in the following line:

``` toml

[project]
readme = "README.md"

```

::::::::::::::::::::::::::::::::::::: callout

In the `README.md` file, developers also usually include in a "contributing" section for new users that are typically outside of the project. The purpose of this section is to encourage new developers to work on the project, while ensuring they follow the etiquette set by the project developers. This may look something like:

```
### Contributing

Contributions to My Python Project are welcome! If you'd like to contribute, please follow these steps:

1. Fork the repository.
2. Create a new branch for your feature (git checkout -b feature/new-feature).
3. Make your changes and ensure tests pass.
4. Commit your changes (git commit -am 'Add new feature').
5. Push to the branch (git push origin feature/new-feature).
6. Create a new Pull Request.
```

::::::::::::::::::::::::::::::::::::::::::::::::


### Licensing 

Following this, it is essential for your software to have a license to emphasise to users what their rights are in regards to usage and redistribution. The purpose of this is to provide the developer with some legal protections, if needed. There are many different open source licenses available, and it is up to the developer(s) to choose the appropriate license. You can explore alternative open source licenses at [www.choosealicense.com](www.choosealicense.com). It is important to note that your selection of license may be influenced by the licenses of your dependencies. 

The most common license used in open source projects is the [MIT license](https://en.wikipedia.org/wiki/MIT_License). The MIT license is permissive, which allows users to freely use, modify, and distribute software while providing a disclaimer of liability.

::::::::::::::::::::::::::::::::::::: callout

The MIT License has the following terms:

Copyright (c) <year> <copyright holders>

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

::::::::::::::::::::::::::::::::::::::::::::::::

As with the `README.md`, you can also add the license to your `pyproject.toml` file as:

``` toml

[project]
license = {file = "LICENSE"}

```

## Releasing Your Software

Once you have prepared all of the material above, you will be in a good position to release your software to an online repository. The most common platform to host your software packages is on GitHub, which uses `git` as the underlying tool to version control your code (note; alternatives are GitLab, BitBucket and SourceForge). 

While the terms `releasing` and `publishing` are commonly used interchangeably, in this course, `releasing` refers to making a version of the software available for download and use, whereas `publishing` refers to the formal announcement and distribution of the software to a wider audience on a platform or marketplace. 

### Git Tags

On GitHub, it is a relatively simple process to create a release of your software by using `Git tags`. `Git tags` are a way of permanently tagging a specific point in your repository's history, which can be used to denote a version that is suitable for others to use. A tag is an immutable reference to a commit (or series of commits), making it simple to identify specific versions of a software, and the tags are commonly identified in conjunction with the Semantic Versioning framework (e.g. v1.0.0). For more information about how GitHub uses tags for software releases, see [releases](https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases).

In general, tagging a release is a 2 step process using Git:

1. Create a tag of a specific point in your software package's history using the `git tag` command that is denoted by a specific version, and upload it to your remote repository using `git push`.

2. Based on your tag, create a release on GitHub of the relevant files in your repository (usually a **zip** or **tar.gz** file), which allows users to download the specific release of your software that corresponds to the time you created your tag.

Collectively, the 2 steps process would look something like:

```bash
$ git tag v1.0.0

$ git push --tags

```
Once you've pushed your tag, you can create a release with the tag you pushed to your remote repository by the following:


<figure style="text-align: center;">
    <img src="fig/git-release.png" alt="Workflow describing how to release a package on GitHub." width="900"/>
    <figcaption><em>Figure 1: Workflow describing how to release a package on GitHub.</em>.</figcaption>
</figure>

::::::::::::::::::::::::::::::::::::: callout

# Deleting a Release

You can also delete a release if you make an error using the following commands:

```bash
$ git tag -d v1.0.0
$ git push origin :refs/tags/v1.0.0

```

The first line simply deletes the tag `v1.0.0` in your local repository, whereas the second line deletes the `v1.0.0 tag` from the remote repository named origin. Note that the colon indicates that you are not pushing any new content to replace the tag; instead, you are specifying that the tag should be deleted. Once you have ran the lines above, you will receive confirmation that the tag has been deleted.


::::::::::::::::::::::::::::::::::::::::::::::::




::::::::::::::::::::::::::::::::::::: challenge

## Challenge 1: Should you always delete a release?

Why might it not be advisable to delete a tag or release, and what alternative actions could you consider instead?

:::::::::::::::::::::::: hint

## Hint

Think about the impact of deleting a tag or release in version control. How might you preserve historical data while managing updates to tags and releases?

:::::::::::::::::::::::::::::::::

:::::::::::::::::::::::: solution

## Solution

Deleting a tag or release in a version control system can disrupt historical tracking and cause confusion for current and future collaborators. Instead of outright deletion, consider tagging the correct commit with a new version number or marking the tag as deprecated with clear documentation. This maintains historical integrity while clarifying the correct state of the codebase. Additionally, communicating changes effectively with team members ensures everyone understands the correct usage of tags and releases for your project.

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

### Creating a release




