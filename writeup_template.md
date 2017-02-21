#**Finding Lane Lines on the Road** 

##Writeup Template

###You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/solidYellowCurve1_lanemask.jpg "Lane mask"
[image2]: ./examples/solidYellowCurve2_normalized.jpg "Normalized"
[image3]: ./examples/solidYellowCurve3_grayscale.jpg "Grayscale"
[image4]: ./examples/solidYellowCurve4_gaussian.jpg "Gaussian Blur"
[image5]: ./examples/solidYellowCurve5_canny.jpg "Canny"
[image6]: ./examples/solidYellowCurve6_region.jpg "Region of interest"
[image7]: ./examples/solidYellowCurve7_hough.jpg "Hough"
[image8]: ./examples/solidYellowCurve8_out.jpg "Result"

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 8 steps.

1. Highlight white and yellow colors with a mask.

![alt_text][image1]

2. Normalize the RGB values.

![alt_text][image2]

3. Convert the image to grayscale.

![alt_text][image3]

4. Use a Gaussian blur.

![alt_text][image4]

5. Use the Canny function to highlight the edges.

![alt_text][image5]

6. Isolate the region of interest.

![alt_text][image6]

7. Use Hough detection on the edges.

![alt_text][image7]

8. Draw lines on the original images.

![alt_text][image8]

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by segmenting the lines into left and right.  Left lines should have a negative slope and right lines should be positive.  I rejected lines with a slope between -0.333 and 0.333.  After segmenting the lines, I used regression on each side to calculate the best fit.  Finally, I used the function for the best fit to create a single line from the bottom of the image to 60% of the height.


###2. Identify potential shortcomings with your current pipeline

* Driving at night.
* Driving in bad weather conditions, like heavy rain or snow.
* Missing lines due to construction.

###3. Suggest possible improvements to your pipeline

* One potential improvement could be to use lines from previous frames if the calculation doesn't work.  It would be a close approximation if not much time has elapsed.
* Another suggestion if the line doesn't work is to calculate based on the speed and trajectory of the car.