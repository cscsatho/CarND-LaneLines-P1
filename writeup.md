# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/solidWhiteCurve.png

---

### Reflection

### 1. Pipeline description

My pipeline consisted of 6 steps:

First, I converted the images to grayscale, then I applied Gaussian blur with a kerner of 3, then this was followed by Canny edge detection (with params of low_threshold=60, high_threshold=180). The fourth step was a region selection, the fifth the Hough Transformation (with params of rho=1, theta=2xPI/180, threshold=20, min_line_len=40, max_line_gap=30), and the last step was drawing the lines on the original image.

In order to draw a single line on the left and right lanes, I created a new method called draw_lines_avg() in order to calculate the average of the given hough lines. In details: I devided the picture into left and right halves, based on the line starts (x1) I grouped the lines, then I calculated the weighted slope and weighted offset for the line leftand right equations. For smoothing line transitions in videos I created a class named LaneFinder(Base) that stores the last valid line equation.

Image showing both all Hough lines (red) and average (green): 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline

Problem could occur when the left and right lines move toward either the left or right half of the image, or when there are several strong lines detected. A more robous caching of previous lines would also help when no good-quality line was detected on the given video image - extrapolation.

### 3. Suggest possible improvements to your pipeline

Possible improvemnts include: filterin out lines that are quite "off" (I already made an attempt on that: the reason I created dictioneries for left and right lines was to calculate a standard deviation so that I could do the filtering for the extremes)

A possible improvement would be to do a color/intensity pre-filering. I also attempted to do this before step 1, but got tired of tweaking the parameters.

In real life a night vision (IR) could also be an advantage.

