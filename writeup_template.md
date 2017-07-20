# **Finding Lane Lines on the Road** 

## Writeup

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I apply Gaussian smoothing and Canny function to the image gray, now we got edges. Next I use a vertices as region of interest in order to reduce influence of noise object such as cars, trees, sky. Finally I called function "hough_lines" to draw a line at images.Thanks to helper function I finally got a not bad result.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by three steps mainly:
* First, for every line I got through function cv2.HoughLinesP, I use slope:((y2-y1)/(x2-x1)), which is >0 or <0, to judge they are left lines or right lines. And then put all left lines into a list, right lines into another list.
* Second, I calculate the average value for two list, in order to find a line to represent all right lines, and also a line for all left lines.
* Third, using the each lines I calculate slope:((y2-y1)/(x2-x1)) and bias to represent the final lane Lines, and extrapolate it to the top and bottom of the region of interest.

And another time-costed work is to fine-tune parameter in some function. For more details and final result you can find in my notebook.


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when there are not only two lines in my region of interest, my code dosen't work, such as challenge videos.

Another shortcoming could be my line sometimes will leap when there are pretty big noise ,for example: a car, appear at my region of interest.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use color information to select lane line in all lines in my region of interest. As for another shortcoming I have no idea how to improve it temporarily, maybe there are still some trick to tune parameter I don't know.
