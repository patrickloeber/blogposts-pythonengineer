---
title: Getting Started with OpenCV in Python
date: 2022-01-29 00:00
description: Learn how to get started with OpenCV in Python.
tags: Python, Computer Vision
path: opencv-python-intro
author: Shweta Goyal
---

In [OpenCV](https://opencv.org/), CV stands for Computer Vision that helps to understand and extract meaningful information from the images and videos. There exist various applications like facial recognition, detecting fingerprints, autonomous vehicles, obstacles avoidance, tumor detection, OCR, MRI, defect detection, etc. and in these and other computer vision applications, you will need OpenCV.

What it does do? It detects features or specific objects from images or videos like faces, eyes, etc. It captures and analyzes the videos like estimating motion, tracking objects, etc, and saves the videos. It performs I/O operations from images or videos.

Let's see what it is and how you can install it on your system.

## Introduction to OpenCV

Open Source Computer Vision Library is the state of the art and one of the most popular computer vision libraries. It supports many languages like C, C++, Python, and Java. OpenCV is well known for its real-time operations and interactive windows capabilities.

OpenCV-Python is a Python API for OpenCV but Python is a bit slower. You can easily extend Python with C/C++, you can create Python wrappers that can be used as Python modules and write code in C/C++ which will make your program computationally intensive. This is a cumbersome task and OpenCV does it for you automatically, it has a few Python scripts. You can learn more about them from [here](https://github.com/opencv/opencv/blob/4.x/doc/py_tutorials/py_bindings/py_bindings_basics/py_bindings_basics.markdown).

OpenCV-Python uses [NumPy](https://numpy.org/) which is an optimization library for numerical operations and can be converted to and from Numpy arrays. It can easily be integrated with other libraries that use Numpy like SciPy and Matplotlib.

## Installation

If you don't have OpenCV on your system, let's see how you can install it.

### Setting up on Windows

You need to have Python to the command line (type cmd in the Run dialog) and pip on your system before installing OpenCV. You can use the command line (type cmd in the Run dialog) for installation in windows.

To check if Python exists, run the following command:

```console
$ python --version
```

This command will tell you the Python version if it exists. To check for pip, run the following command:

```console
$ pip -V
```

Pip is a system that installs or manages software packages/libraries written in Python. This command will tell you the location of the pip installed in your system and the version.

To install OpenCV, it can directly be installed using pip by command line. Execute the following command:

```console
$ pip install opencv-python
```

This command will install all the necessary data or information required. To check the version, run the following command:

```python
import cv2
print(cv2.__version__)
```

### Setting up on Ubuntu

Python comes pre-installed on Ubuntu, so we directly install OpenCV now. Open the terminal (as root user) and run the following command:

```console
$ sudo apt-get install python3-opencv
```

To check if it installed properly, execute the following command:

```python
import cv2
print(cv2.__version__)
```

### Setting up with Anaconda Environment

Anaconda is open-source software that is used for large data processing and heavy computing, it contains jupyter notebooks, spyder, etc.

For Anaconda installation, you need to have a minimum of 3 GB disk space on your system but for miniconda, 400 MB disk space will work. You should have a 32-bit or 64-bit system.

For installation, go to their main website and install it with the default setting.

After you are done with the installation, open the Anaconda Prompt (Start Menu / Anaconda3 / Anaconda Prompt). First create a new environment named *opencv* and activate it:

```console
$ conda create -n opencv
$ conda activate opencv
```

Then execute the following command:

```console
$ pip install opencv-python
```

Note: `conda install` can also be used. More information can be found [here](https://anaconda.org/conda-forge/opencv):

```console
$ conda install -c conda-forge opencv
```

To learn more about Anaconda, you can read [this](/posts/anaconda-basics/) article on our website.

## End Notes

OpenCV has been tremendously used in various applications and helps to make our tasks easier in computer vision, image processing, and machine learning. This tutorial gives you an overview of OpenCV and helps you to set up the library on your system.
