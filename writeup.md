# **Finding Lane Lines on the Road** 

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps.
1. Convert the images to grayscale
![alt text][grey_solidWhiteCurve]
2. Apply Gaussian smoothing
![alt text][gaussian_solidWhiteCurve]
3. Apply the Canny algorithm to find the edges of lanes lines in the image
![alt text][canny_solidWhiteCurve]
4. Define a four-sided polygon and apply it to the masked edge image so that only the edges within the polygon are considered as lanes and all the edges outside the polygon are ignored.
![alt text][polygon_solidWhiteCurve]
5. Run Hough on the edge detected image to get all the detected lines and draw the lines on the edge images
![alt text][hough_solidWhiteCurve]

[grey_solidWhiteCurve]: https://github.com/ChengJoyceJi/CarND-LaneLines-P1/blob/master/test_images_output/grey_solidWhiteCurve.jpg
[gaussian_solidWhiteCurve]: https://github.com/ChengJoyceJi/CarND-LaneLines-P1/blob/master/test_images_output/gaussian_solidWhiteCurve.jpg
[canny_solidWhiteCurve]: https://github.com/ChengJoyceJi/CarND-LaneLines-P1/blob/master/test_images_output/canny_solidWhiteCurve.jpg
[polygon_solidWhiteCurve]: https://github.com/ChengJoyceJi/CarND-LaneLines-P1/blob/master/test_images_output/polygon_solidWhiteCurve.jpg
[hough_solidWhiteCurve]: https://github.com/ChengJoyceJi/CarND-LaneLines-P1/blob/master/test_images_output/hough_solidWhiteCurve.jpg

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by
1. Calculate the slope of each line segment: slope = (y2-y1)/(x2-x1). If the slope is positive, it belongs to the right lane. If the slope is negative, it belongs to the left lane.
2. Get all the x values and y values of all the points on the lane, fit them into a linear regression modal to find the fitted coefficients.
3. Extrapolate the estimated y value from x values of the two ends of the lane, and draw the line from these two points as the estimated lane.


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when `lines` returned from `HoughLinesP` is empty. In this case I have hard coded two points based on observations and connect these two points to get the predicted lane, which can go wrong.

Another shortcoming could be if there are another signicant line within my defined polygon region and it got detected by Canny, then this line will signifcantly affect the lane I draw.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to use the predicted lanes from the previous image if there's no lines detected in the current image. 

Another potential improvement could be to better define the polygon region.
