# **Finding Lane Lines on the Road** 

[grayscale]: ./test_images/grayscaled_img.png


### 1. Software Pipeline
My pipeline consists of the following 9 steps.
For each image in the video, 
1. Convert image to grayscale.
2. Run Canny Edge Detector to produce edge image.
3. Mask edge image with spatial region of interest.
4. Mask edge image again with pixel value region of of interest.  (Only edges from yellow or white pixels are held.)
5. Run Hough Line Detector to detect lines from the masked edge image.
6. Classify lines from the left half of the image as left lane lines and lines from the right half of the image as right lane lines.
7. Filter lines based on the slope of the line. 
8. Fit a single line on the lines from the left lane lines and another single line on the lines from the right lane lines.  RANSAC is used to fit a line which improves the line fitting using only the inliers.
9. Overlay left and right lane lines on the original image for visualization.


[grascale]


### 2. Potential shortcomings with current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Possible improvements to current pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
