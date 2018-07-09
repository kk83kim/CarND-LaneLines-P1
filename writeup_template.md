# **Finding Lane Lines on the Road** 

[blurred]: ./test_images/blurred_img.png
[edge]: ./test_images/edge_img.png
[masked_spatial]: ./test_images/masked_spatial_roi_img.png
[masked_color]: ./test_images/masked_color_roi_img.png
[line]: ./test_images/line_img.png
[overlayed]: ./test_images/overlayed_img.png


### 1. Software Pipeline
My pipeline consists of the following 9 steps.

For each image in the video, 

1. Convert image to grayscale and blur using gaussian filter.

![alt text][blurred]

2. Run Canny Edge Detector to produce edge image.

![alt text][edge]

3. Mask edge image with spatial region of interest.

![alt text][masked_spatial]

4. Mask edge image again with pixel value region of of interest.  (Only edges from yellow or white pixels are held.)

![alt text][masked_color]

5. Run Hough Line Detector to detect lines from the masked edge image.
![alt text][line]

6. Classify lines from the left half of the image as left lane lines and lines from the right half of the image as right lane lines.
7. Filter lines based on the slope of the line. 
8. Fit a single line on the lines from the left lane lines and another single line on the lines from the right lane lines.  RANSAC is used to fit a line which improves the line fitting using only the inliers.
9. Overlay left and right lane lines on the original image for visualization.

![alt text][overlayed]


### 2. Potential shortcomings with current pipeline
There are at least a couple of shortcomings with the current approach.  

First, masking using the pixel color actually does not help as much as I hoped to be because the edges detected from the blurred image are the the pixels in the between the sharp change between the background and the white or yellow lanes.  Thus, although some edges are from the actual edges of the lanes, its pixel color is not necessary white or yellow.

Second, this pipeline is not very robust to different light conditions.  I tested on the optional challenge video and it did not perform very well.


### 3. Possible improvements to current pipeline
One potential solution to the first shortcoming mentioned above is to look at the neighborhood of pixel colors around the edges instead of the pixel color of the actual edge.

For the second shortcoming, a few additional heuristics could be helpful such as keeping a history of detected lane lines.  Using the position and the slope of the past lane lines could be used to verify if the current detected lane lines are accurate or not.
