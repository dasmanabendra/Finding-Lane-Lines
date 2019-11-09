# **Finding Lane Lines on the Road** 

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


### Reflection

### 1. Pipeline description 

My pipeline consisted of 5 steps. 
1) Convert image to grayscale
2) Perform Gaussian smoothing 
3) Perform Canny edge-detection
4) Mask the edges
5) Perform Hough transform
6) Draw lines on original image

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

The left and right line are obtained from averaging the set of lines on each side. 
Only a subset of lines from the hough_lines are considered to filter out false positives:  
    1) slopes are within a specified range
    2) the x intercept at the bottom of the screen lies inside the image
The top and bottom limits are predefined.
The slope and x-intercept on the top and bottom limits are calculated.


### 2. Potential shortcomings 


Potential shortcoming would be what would happen when ... 
1) There are frames/images when no lines are detected.  The lines are not drawn for these frames.
2) Lanes with a small radius of curvature have not been tested. This would be scenario when a significant steering command will be required but the current pipeline may fail to detect a lane :(


### 3. Possible improvements 

A possible improvement would be to
1) In the video steam the continuity of the lane lines in time domain has not been utilized.  The left and right lines from the previous frame can be passed to draw_lines to filter out the lines that are not similar (slope and intercept within a tollerance) to the lineas from the previous frame.    

2) A predictor (similar to ones used in numerical time integrators) algorithm can also be devised where the lineas (slope and intercept) from the previous few frame can be extrapolated to predict lines in the current frame.  This can be helpful for frames where the inage quality becomes poor (e.g. poor lighting, missing lanes marks).  

3) Instead of representing lanes with lines (infinite curvature) a spline (finite curvature) can also be employed to improve accuracy of lane detection.
