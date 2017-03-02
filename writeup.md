#**Finding Lane Lines on the Road** 

##Writeup by Ernesto Cañibano

###This is the writeup associated with the first project of the Term 1, of the Self-driving Car Nanodegree

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

My pipeline consists of several steps, all included in the funcion *process_image()*. In this section i will describe in detail each step and how i have reached them. I will use one image as an example to explain all process.


* **Conver the images to grayscale**. It is only a transformation usign the function grayscale()

  ![alt text][image2]

* **Edge detection**. Next step is edge detection using Canny Edge detection. 

  First, i used the function **gaussian_blur()** with **kernel_size=3**. After several iterations i found that this value works properly. This value improve the the noise but keeps the lines sufficiently defined.

  After that, the function **canny()** with values: **low_threshold=50** and **high_threshold=200**. I obtained these values performing several iterations and observing the result.

  ![alt text][image3]

* **Mask the image**. Before to do the Hough tranformation, I applied the mask over the image to reduce amount of the calculations. To achieve a good mask, I drew a polygon over all the test images usign the original funcion **draw_lines**. When i had a mask a valid for all the images, I got the values of ther vertices to use them in the pipeline. In the image below, it is possible to see the polygon drawn over one the images.

  ![alt text][image4]

  Finally, in the following image, it is showed the mask applied over the result of the edge detection.

  ![alt text][image5]  
  
* **Hough Transformation**. This step is performed with the function **hough_lines()**. 

    First, the funcion perform the Hough Transformation. After several iterations with all test images, I decided use the following values: **rho=2**, **theta=pi/180**, **threshold=20**, **min_line_len=60** and **max_line_gap=35**. After that, the function **draw_lines()** draw all the lines obtained over the image. In the image below is showe the result of this transformation, usign the original **draw_lines** over one of the test images.
  
    ![alt text][image6]  
	
* **Average and extrapolation of the lines**. Once the algorithm is working properly, I added a parameter to the funcion **draw_lines()** to improve the line detection. 

  The modification consist on the folling stages:
  * Deteccion of lines with positive and negative slope. 
  * Using the slope, estrapolate all lines until reaching the vertical limits of the masking area.
  * Calculate the average of the lines with positive slope and with negative slope. The first average generate the right line of the road and the second the left line of the road.
  
  ![alt text][image7]
  

###2. Identify potential shortcomings with your current pipeline


The pipeline works fine with all test image and with two test videos.  

With the video **challenge.mp4**, it works too, but it fails when the color of the road is less dark. 

I think the pipeline can fail in some cases such as:
* Another white/yellow marks painted in the road like arrow, letters an signals.
* When the road asphalt is not dark enough.
* When the car approaches to very tight curves.


###3. Suggest possible improvements to your pipeline

I think the pipeline could be improved by appliying some time of color selection or color enhanced at the beginning, before converting to grayscale. In this way the effect of color of the road.

To avoid the effect of another marks in the road, the masking region could be defined dinamically, doing several iterations, approaching it to the real shape of the lines in the Road.

Finally to improve the behaviour in the curves, an improvement coul be to apply a more complex extrapolation with curve lines. 


