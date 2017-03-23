#**Finding Lane Lines on the Road** 

##Writeup

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/solidYellowCurve_result.png "Example"

---

### Reflection


My pipeline consisted of 6 steps:
* convert imag to grayscale,
* apply gaussian smoothing (kernel size = 7),
* apply canny algorithm (low threshold = 50, high = 145),
* create and apply mask for edges image (four sided polygon, values depend on image size)
* apply hough transform on masked edges image
* draw detected lines over original image

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by adding following steps
* calculating center point for each line
* calculating slope of each line
* if slope is negative AND center point X coordinate is left from image center, center point is added to centerPointsLeft array
* if slope is positive  AND center point X coordinate is right from image center, center point is added to centerPointsRight array
* applying RANSAC to fit a line through left center points (if their amount is higher than 5)
* applying RANSAC to fit a line through right center points (if their amount is higher than 5)
* getting predictions for X coordinates of desired minimum and maximum Y coordinates for both lines (left and right)
* drawing solid left (red) and right (blue) line
* additionaly drawing small green circles for center points used for fitting lines with RANSAC

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


###3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...