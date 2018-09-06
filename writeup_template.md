# **Finding Lane Lines on the Road** 
---

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road:
    - Applying on what I learned from the lesson, the arrangement of the functions, and the parameters' tunning.
    - Edit the output of the hough lines to form TWO Red Lines roughly representing the Two lane lines.
    - Test On 6 images.
    - Test on 2 videos.
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/solidWhiteRight.jpg "SolidWhiteRight"
[image2]: ./test_images_output/whiteCarLaneSwitch.jpg "whiteCarLaneSwitch"
[image3]: ./test_images_output/solidYellowLeft.jpg "solidYellowLeft"
[image4]: ./test_images_output/solidYellowCurve2.jpg "solidYellowCurve2"
[image5]: ./test_images_output/solidWhiteCurve.jpg "solidWhiteCurve"
[image6]: ./test_images_output/solidYellowCurve.jpg "solidYellowCurve"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps:
    - Convert the images to grayscale.
    - Smooth using Guassian_blur.
    - Extract the edges using Canny Algorithm.
    - Extract the region of interest (a polygon where the Lanes most probably exist).
    - Connect the pixels in this region to form meaningful discrete lines (hough lines).
    - Put the lines on the source image.


In order to draw a single line on the left and right lanes, I ignored the draw_lines() function and renamed the hough_lines() function to draw_two_lines() and added my solution there which goes like this: 

- From the hough lines store each line's slope and separte them according to it's sign in two different arrays, also store the C value in each line's equation (y=xm+C) 
- Calculate the median value of each Array (The positive slopes array, the negative slopes array and the C arrays) 
- Calculate Two points for each Required Red Line through the equation (y=xm+c) knowing the m_median,c_median and giving y values either 320 (approximately the middle of the frame) and im.shape[0] (y's biggest value= the lowest point in the frame).
- Draw the Two lines and  put them on the source image.

Here are the test images output: 

![alt text][image1]
![alt text][image2]
![alt text][image3]
![alt text][image4]
![alt text][image5]
![alt text][image6]


### 2. Identify potential shortcomings with your current pipeline


- If there are so many shadows on the road, the hough lines won't be accurate enough.
- If there's a strong curve (like a U turn) or like when driving around a hill, the region of interest will still be valid, but the straight lines won't work.  



### 3. Suggest possible improvements to your pipeline

- Give it a range of slopes to accept it only./ Get rid of the shadows first or use the property of lane lines of being yellow/white  (very bright).
- At some situations like the turning or the hill examples we will need to draw curves instead of lines (I think).