# **Finding Lane Lines on the Road** 
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)
   
<img src="examples/laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

## Writeup 
---
**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

---

### Reflection

### 1. Describe the pipeline of the draw_lines() function.

My pipeline consisted of the following steps:
1. Convert the images to grayscale using the helper function grayscale()
2. Blur the image using Gaussian smoothing
3. Apply Canny Edge Detection 
4. Define vertices
5. Apply an image mask by using the helper functionregion_of_interest()
6. Run Hough Transform to find lines in image
7. Apply weighted_line() to combine initial image with the image after Hough Transform

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by:
1. Seperate line segments as left and right lines
2. For each line, calculate average slopes and intercepts
3. Calculate y_min, y_max
4. For left and right lines, calculate x_min and x_max using intercept, slope
5. Draw a line using (x_min, y_min) and (x_max, y_max)

Here is the examples of the final output videos:
<script src="https://github.com/duongquangduc/Udacity-CarND-LaneLines-P1/blob/master/test_videos_output/solidWhiteRight.mp4"></script>
[![Watch the video](https://github.com/duongquangduc/Udacity-CarND-LaneLines-P1/blob/master/test_videos_output/solidWhiteRight.mp4)]

### 2. Identify potential shortcomings with your current pipeline

One potential shortcoming of this solution is that the lane line could be wrong when running the algorithm on different videos or different roads. This could be due to the initialized values of the parameters like KERNEL_SIZE, LOW_THRESHOLD, HIGH_THRESHOLD, RHO, THETA, MIN_VOTES, MIN_LINE_LEN, MAX_LINE_GAP, BOTTOM_SHIFT, TOP_SHIP are not suitable. This is also one of the challenge for this problem when I have to manually try with different values.


### 3. Suggest possible improvements to your pipeline

There are several improvements that I could try in future.
1. First, I can re-preprocess the original image, not just convert it to grayscale but different channel and increase its contrast.
2. Second, try different algorithms that can fix the issues of identifying the proper values for the mentioned parameters.
