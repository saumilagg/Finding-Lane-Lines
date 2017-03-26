#**Finding Lane Lines on the Road** 

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]:./test_images_output/grayscale.png "Grayscale"

[image2]:./test_images_output/cannyOutput.png "CannyEdges"

[image3]:./test_images_output/ROI.png "ROI"


[image4]:./test_images_output/houghTransform.png "HoughTransform"

[image5]:./test_images_output/solidYellowCurve2.1.png "solidYellowCurve"

[image6]:./test_images_output/solidWhiteRight2.png "solidWhiteRight2"

---

### Reflection

###1. Describe your pipeline. 

My pipeline consists of 5 steps.

1) Converting the image to grayscale

![alt text][image1]

2) Gaussian smoothing to supress any noise in the image

Selected a kernel size of 5 to smooth over a large area

3) Setting the threshold values and applying canny for edge detection 

![alt text][image2]

4) Select region of interest

![alt text][image3]

5) Apply Hough Transform

![alt text][image4]

In-order to draw solid lines on the image I modified the draw_lines function. My logic was something on these grounds: I first determined the line equation in
the form y = mx + b; by plotting my region of selection. This gave me an idea of slope and points lying on/above/below the line. Now I kept this slope(m) from
original line equation  as an initial start value for averaging slope. So for any new points x1,y1,x2,y2 on the line, I calculate the slope and keep it in the
range delta (which is my case is 0.85). The final line is drawn after iterating through these points and selecting the best possible combination.

Note: For final image results after changing the draw lines function look for ./test_images_output/filename2.png. where "filename" is the image name with a "2" 
as suffix. 

Some of the final results look like this: 

![alt text][image5]

![alt text][image6]
 
###2. Identify potential shortcomings with your current pipeline

The pipeline was designed according to the image shape parameters which were the same for all images. A change in image shape would possibly lead
to unexpected results. However the steps for pipeline and detecting lane is robust. 

Also, other shortcoming is in video i.e continuous stream of images; we can clearly see the red lines marking the lane but sometimes a few red lines are 
thrown here and there all over the video. This is a strange senario and might need optimization in thresholds. 
 

###3. Suggest possible improvements to your pipeline

A possible improvement would be to rewrite the draw lines logic. Currently I have assumed certain points for marking lane and I'm calculating 
the best fitting line around those parameters. This is not a very efficient way and the challange video clearly denomstrates that where the algorithm fails. 
A possible solution would be using max and min, x & y coordinated and connect them using a polyfit fucntion maybe. Or I might might have to come up with a 
mathematical fucntion to extrapolate the lines which would consider the line length as well! I think there are a lot of different ways to do this.  

Another potential improvement could be to optimize the parameters in such a way that any image shape could be adjusted and correct lanes could me marked down. 

I hope to commit changes as I work on them in the future. 
