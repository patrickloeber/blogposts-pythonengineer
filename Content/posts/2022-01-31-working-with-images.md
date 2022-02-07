---
titlt: Working with Images in OpenCV using Python
date: 2022-01-31 00:00
description: Basic operations with images in OpenCV using Python
tags: Python OpenCV Images
path: 
author: Shweta Goyal
---

# Working with Images in OpenCV using Python

OpenCV is one of the most common libraries that you need in any computer vision or image processing task. Before applying different filters for image processing or to perform any image-related task, you must know how to read an image, display an image, or write an image.

OpenCV comes with inbuilt functions to perform these basic operations. Let’s see how you can use these functions in your task.

Before performing any operation, make sure you have OpenCV, Numpy, and Matplotlib (optional) in your system. OpenCV uses Numpy in the backend and Matplotlib is required for displaying images.

This is the original image that is going to be used here:

Photo by Nick Fewings on Unsplash

## Reading an Image

OpenCV has an inbuilt function that will read/load/open an image which is `cv2.imread()`. Let’s see the syntax:

`cv2.imread(Pathname, Flag)`

It consists of two arguments:

- **Pathname:** It contains the pathname of the image to be read. Make sure your image should be in the same directory or the full pathname of the image should be specified, otherwise you will get an empty matrix.

- **Flag:** It is an optional argument. It sets the format of the image in a way you want to be read. There are three types of flags:

      - **cv2.IMREAD_COLOR or 1:** This will read the image in a colored mode by removing any transparency from the image. OpenCV loads the color image in a BGR 8-bit format. This flag is used by default.

      - **cv2.IMREAD_GRAYSCALE or 0:** This will read the image in a grayscale mode.
 
      - **cv2.IMREAD_UNCHANGED or -1:** This will read the image as it is including the alpha channel if it is present.

Let’s see how you can read an image by using three different flags:

```python
Color = cv2.imread(‘dog.jpg’, 1)
Grayscale = cv2.imread(‘dog.jpg’, 0)
Unchanged = cv2.imread(‘dog.jpg’, -1)
```

## Displaying an Image

OpenCV has an inbuilt function that will display an image in a window which is `cv2.imshow()`. Let’s see the syntax:

`cv2.imshow(WindowName, Image)`

It consists of two arguments:

- **WindowName:** It specifies the name of the window which contains the image. This will help you to display multiple images at a time, you can specify different window names for every image.
- **Image:** It is the image that will be displayed.

There are other functions that are used along with this function.

- **cv2.waitKey():** It will display the window on the screen for the time period which is in milliseconds. The value should be a positive integer. If the value is 0, It will hold the window indefinitely until you press a key.
- **cv2.destroyAllWindows():** It will destroy all the open windows from the screen and from the memory which was created.
- **cv2.destroyWindow():** It will destroy the specific window. The argument will be a window name that you want to be destroyed.

## Writing an Image

OpenCV has an inbuilt function that will write/save an image to the given path which is `cv2.imwrite()`. It will save your image in the working directory. Let’s see the syntax:

`cv2.imshow(FileName, Image)`

It consists of two arguments:

- **FileName:** It contains the name of the file which should be in the .jpg, .png, etc format.
- **Image:** It is the name of the image that will be saved.

To sum it up, you will see an example that will load an image in grayscale, displays it, and then saves it.

```python

import cv2

# Reading an image
Gray = cv2.imread("dog.jpg", 0)

# Display an image in a window
cv2.imshow('Grayscale Image', Gray)

# Wait for a keystroke 
cv2.waitKey(0)

# Destroy all the windows
cv2.destroyAllWindows()

# Write an image
cv2.imwrite('GrayScale.jpg', Gray)
```

Here, you can see the displayed image is in a grayscale mode which is different from the original image.

Let's see another example that will load an image in colored mode.

```python

import cv2

# Reading an image
Color = cv2.imread("dog.jpg", 1)

# Display an image in a window
cv2.imshow('Colored Image', Color)

# Wait for a keystroke
cv2.waitKey(0)

# Destroy all the windows
cv2.destroyAllWindows()

# Write an image
cv2.imwrite('Colored.jpg', Color)
```

Here, you can see the displayed image is in a colored mode which is somewhat similar to the original image.

End Notes

This article will help you to start your OpenCV journey. You learned how to read an image, how to display it, and how to save it in your local directory. There are many other operations you can perform on images.
