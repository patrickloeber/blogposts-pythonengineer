---
title: Working with Videos in OpenCV using Python
date: 2022-02-13 00:00
description: Basic operations with videos in OpenCV using Python.
tags: Python, Computer Vision
path: opencv-videos
author: Shweta Goyal
---

OpenCV has been used in various video-related tasks like in drones, robots, car navigation and control, surveillance cameras, video tracking, embedded systems like Aurdino and Raspberry Pi, etc.

A video is a sequence of frames and each frame is an image. It is displayed at a speed of frames per second. In this article, you will learn how to capture a video, display a frame and save a video.  

This is the video taken from [Kaggle](https://www.kaggle.com/kmader/drone-videos?select=Bluemlisalphutte+Flyover.mp4).

## Reading a Video

There are two ways you can read a video either from a file or from a webcam. OpenCV provides a *VideoCapture* object to perform this operation. Let’s see the syntax:

```python
cv2.VideoCapture(filename)
```

Here, you can give the name of the file if it is in the same directory where your program is or you can provide the full path if your file is in a different directory.  

Let’s see an example by reading a video from a file:

```python
import numpy as np
import cv2

# Reading a video from file
cap = cv2.VideoCapture('Flyover.mp4') 

while(cap.isOpened()):
    
    # capture frame-by-frame
    ret, frame = cap.read()
    if ret == True:

        # Display a frame
        cv2.imshow('Frame', frame)

        if cv2.waitKey(25) & 0xFF == ord('q'):
            break

# Release the capture object
cap.release()

# Destroy all windows
cv2.destroyAllWindows()

```

After you have captured the video, you can use the `isOpened()` method to check if your video is successfully opened. Otherwise you will get an error message. It returns a boolean value (True/False) to confirm if the provided video stream is valid or not.

OpenCV also provides a method through which you can access some properties of the video, you can use the `cap.get(propId)` method.

It consists of a single argument:

- *propId:* It is the property of the video. It contains an enumerated list of options, you can access the full list from [here](https://docs.opencv.org/2.4/modules/highgui/doc/reading_and_writing_images_and_video.html#videocapture-get). You can provide numeric values or you can pass the full name. Here, the number denotes the property of the video.

If you want to modify the existing value, you can use the `cap.set(propId, value)` method.

It consists of two arguments:

- *propId:* It indicates the property of the video.
- *value:* It indicates the value that you want to modify.

For example, if you want to check the width and height of the frame you can use `cap.get(3)` and `cap.get(4)`. It will give you by default 640x480. If you want the value 320x240, you can modify it by using `ret = cap.set(3, 320)` and `ret = cap.set(4, 240)`.

In the above code, the `cap.read()` method is used to capture each frame from a file by creating a loop and reading one frame at a time. It returns a tuple where the first element indicates a boolean value if it is true that means the frame is captured correctly and the second element is the video frame.

You can use the `imshow()` method to display a frame in a window. You can also use the `waitKey()` method to pause the video frame and it will wait until you press the key. In the above code, it will wait until you press the `q` key and then you exit the loop.

You can also use a webcam by specifying the device index which is just the number of the camera. If you pass 0 then it is for the first camera, 1 is for the second camera, and so on. Let’s see the syntax:

`cv2.VideoCapture(0)`

The rest of the code is the same, you just have to replace the video file name with your device index.

## Writing a video

OpenCV has a *VideoWriter* object that helps to save the video. You can write the file in any format once you provide the right arguments. Let’s see the syntax:

```python
cv2.VideoWriter(Filename, Fourcc_code, FrameRate, FrameSize)
```

It consists of four arguments:

- *Filename:* Name of the output file
- *Fourcc\_code:* This is a 4-byte code that specifies the video codec. It is platform-dependent. You can access the full list at [fourcc.org](https://www.fourcc.org/codecs.php). It is used to compress frames. FourCC code is written as `cv2.VideoWriter_fourcc(‘X’, ‘V’, ‘I’, ‘D’)` or `cv2.VideoWriter_fourcc(*’XVID’)` for XVID.
- *FrameRate:* Frame rate of created video stream which is in fps (frame per second).
- *FrameSize:* It is the size of the video frames which is width and height.

Let’s see the implementation by capturing a video from a file and writing it in a output file:

```python
import numpy as np
import cv2

# Reading a video from file
cap = cv2.VideoCapture('Flyover.mp4')

# Initialize VideoWriter object
fourcc = cv2.VideoWriter_fourcc(*'XVID')
out = cv2.VideoWriter('Output.mp4', fourcc, 10.0, (1280, 720)) 

while(cap.isOpened()):
    
    # capture frame-by-frame
    ret, frame = cap.read()
    if ret == True:
        
        # Write the frame to output file
        out.write(frame)

        # Display a frame
        cv2.imshow('Frame', frame)

        if cv2.waitKey(25) & 0xFF == ord('q'):
            break

# Release the capture objects
cap.release()
out.release()

# Destroy all windows
cv2.destroyAllWindows()
```

## End Notes

OpenCV comes with many tools and inbuilt functions that will make our tasks easier, whether it will be images or videos. This article covered two such functions: **cv2.VideoCapture()** and **cv2.VideoWriter()**. The goal of this article will give you a start and now you can try this on another video or try to perform this using webcam.
