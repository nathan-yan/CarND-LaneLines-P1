# **Finding Lane Lines on the Road** 

## Writeup Template

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

My pipeline consisted of 6 steps:
1. I converted the image into greyscale
2. I performed Canny edge detection on the greyscale image 
3. I sectioned the image so only the region of interest was showing. The vertices were: lower left corner, center of image, lower right corner
4. I performed a hough transform
5. I performed a second hough transform, this time with a much larger min_line_len (to eliminate small, stray line segments), and a much larger max_line_gap (so that line segments on the same line could be connected), as well as a much larger threshold (to further filter out small, stray line segments). 
6. The candidate lines then went through a simple clustering algorithm that grouped lines within a certain distance_threshold apart. Lines with slopes less than .3 were also deleted. 

I modified the hough_lines function so that it would return both the hough image, as well as the lines it detected. This was useful for the clustering section of the pipeline. 

I also added a *dist* function that found the distance between two points. 

### 2. Identify potential shortcomings with your current pipeline

My pipeline makes a couple assumptions about lane lines that do not generalize perfectly to the real world. For example, I assumed that lines with slope less than .3 were artifacts, and could not be real lane lines. This makes sense, and would usually be a pretty robust filter, but it is possible that there is a lane line with slope less than 0.3. 

### 3. Suggest possible improvements to your pipeline

I was considering having lane line detections to extend all the way to the bottom of the image, by taking the slope of the line, and making the end point of the line have a y-coordinate of image.shape[0]. 

Extending the pipeline to be able to consider curved lines, so that curves in the road can still be graphed. 
