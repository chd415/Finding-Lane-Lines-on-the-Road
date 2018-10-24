# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

In this project, we are asked to write the code ourselves to find the lines of a self-driving car initially based on the still pictures and then using the video provided. Even though analysising videos seems to be harder, but the pipeline of the whole process should be same. The video is just a sum of the still pictures. So I will take the still picture as an example.

Initiall, we are given this picture which does not have any ditected lines yet:
![Initial picture][test_images/solidWhiteRight.jpg]

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

1. convert the colorful picture into gray one: gray = grayscale(image)
2. suppress noise and spurious gradients: gaus = gaussian_blur(gray, 5)
3. use canny function to detect edges: edges = canny(gaus, 50,150)
4. get the area where there most likely to contain the lines to be detected: imshape = image.shape; vertices = np.array([[(0,imshape[0]),(450, 320), (500, 320), (imshape[1],imshape[0])]], dtype=np.int32); masked = region_of_interest(edges, vertices)
5. based on the region detected in step4, to get the lines only in this certain region: line_image = hough_lines(masked, 3, np.pi/180, 20, 15, 20)
6. finally, show the picture with the initial one and this mask with the detected lines: result = weighted_img(line_image, image).
If you'd like to include images to show how the pipeline works, here is how to include an image: 

![Output picture][test_images_out/outsolidWhiteCurve]


### 2. Identify potential shortcomings with your current pipeline


The shortcomings in this current project is that:
1. those white dash lines in the initial pictures cannot be redrawed as a solid red line. The drawed red line can onlt appeared where there are initial white lines. 
2. for the yellow line detected, there are still many noise occured in the output pictures.


### 3. Suggest possible improvements to your pipeline

Acoording to the shortcomings stated previously, the potential improvements of these shortcomings are:
1. use some other packages that may suit with this problem better. 
2. modifing some threshold values to improve the quitity of the mask and decrease the noise.  