#**Finding Lane Lines on the Road** 

##Writeup Template

###You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images/solidWhiteCurve.jpg "Original"
[image2]: ./examples/solidWhiteCurve_gray.jpg "Grayscale"
[image3]: ./examples/solidWhiteCurve_edges.jpg "Edges"
[image4]: ./examples/solidWhiteCurve_mask.jpg "Mask"
[image5]: ./examples/solidWhiteCurve_masked.jpg "Edges Masked"
[image6]: ./examples/solidWhiteCurve_hough.jpg "Hough Transformation"
[image7]: ./examples/solidWhiteCurve_average.jpg "Lines Modification"


---

### Reflection

###1. Pipeline explanation

My pipeline consists of several steps, all included in the funcion process_image(). In this section i will describe in detail each step and how i have reached them. I will use one image as an example to explain all process.
![alt text][image2]

* Conver the images to grayscale. It is only a transformation usign the function grayscale()
![alt text][image2]
* Edge detection. Next step is edge detection using Canny Edge detection. First i use the function gaussian_blur() with kernel_size=3. 
![alt text][image3]
* Mask the image.
![alt text][image4]

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


###3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...