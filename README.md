# **Finding Lane Lines on the Road** 
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

<img src="examples/laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

Overview
---

When we drive, we use our eyes to decide where to go.  The lines on the road that show us where the lanes are act as our constant reference for where to steer the vehicle.  Naturally, one of the first things we would like to do in developing a self-driving car is to automatically detect lane lines using an algorithm.

In this project I will detect lane lines in images using Python and OpenCV.  OpenCV means "Open-Source Computer Vision", which is a package that has many useful tools for analyzing images.  


**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road



### Reflection

### 1. Describe the pipeline. As part of the description, explain how to modify the draw_lines() function.

My pipeline consisted of 5 steps:

-(i)First I converted image to grayscale.

-(ii)Smoothening of image by Gaussian filters

-(iii)Edges are detected using Canny filter

-(iv)Now we have the image with edges detected all over the image but our focus is on the lane edges.So we will use polyfunction to specify our region of interest.

-(v)So we have features from the region of interset,now we have to detect lines within this region.For that we will be using Hough transform.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by calculating the slope of lines detected by Hough transform.Since our Y dimension is increasing downwards,Negative slope will be corresponding to left lane and positive slope will be for right lane.If the lines are vertical, then it is neglected say for eg zebra lines are not considered.By taking weighted average of the slopes and intercepts of left and right lanes,we have the right metric to extrapolate the line from fixed points in image by finding xcoordinates in base by slope equation.

### Results

### Input image
![alt text](https://github.com/hari1106/Lane-Detection-Autonomous-Car/blob/master/test_images/solidYellowLeft.jpg)
### Preprocessing
![alt text](https://github.com/hari1106/Lane-Detection-Autonomous-Car/blob/master/writeup_images/filters.png)

### Hough output
![alt text](https://github.com/hari1106/Lane-Detection-Autonomous-Car/blob/master/writeup_images/hough.png)

### Final Output
![alt text](https://github.com/hari1106/Lane-Detection-Autonomous-Car/blob/master/writeup_images/final.png)

### Video
[Video Link](https://github.com/hari1106/Lane-Detection-Autonomous-Car/blob/master/test_videos_output/solidWhiteRight.mp4)

### 2. Identify potential shortcomings with the current pipeline

>One potential shortcoming would be what would happen when there are curves or turnings where lines can intersect.

>Another shortcoming could be the region of interest approach which depends on the position of camera and also in real life situation there will be multiple objects in the road which can block the lanes and also reflections may lead to false detection.


### 3. Suggest possible improvements to the pipeline

>A possible improvement would be to find best regions of interest and use HSV color transformation.

>Another potential improvement could be to train a deep learning model with different scales and augmented images of lanes so that the model won't be dependent on the position of camera or region of interest specific.
