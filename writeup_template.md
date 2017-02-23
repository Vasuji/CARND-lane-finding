#**Finding Lane Lines on the Road** 

##Writeup Template

###You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function and added the property of 

My pipeline consisted of 5 steps. 


#### Step-I:

First, I converted the images to grayscale, using  ```grayscale``` helper function

```
grey_image = grayscale(image)

```
![1](https://github.com/Vasuji/carnd-project1/blob/master/pipeline_images/1grey_image.jpg?raw=true)

#### Step-II:

Insecond Step I added the property of gaussian blur to the image. Eventhough it was optional step because ```Canny``` function is going to use ```5 x 5``` kernel size for adding gaussian noise, I added this to shee effect.

```
gaussian_blur_image = gaussian_blur(grey_image, kernel_size=3)

```
![2](https://github.com/Vasuji/carnd-project1/blob/master/pipeline_images/2gaussian_blur_image.jpg?raw=true)

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

#### Step-III:
In third step, I applied canny helper function to find sharp edges. Sharp edges are because of change in pixcel values which we call gradient.
```
 canny_image = canny(gaussian_blur_image,\
                    low_threshold=50,\
                    high_threshold=150)
 ```
![3](https://github.com/Vasuji/carnd-project1/blob/master/pipeline_images/3canny_image.jpg?raw=true)

#### Step-IV:
In fourth step, I selected the region of interest,
```
 masked_image = region_of_interest(canny_image,\
                                  vertices=vertices0 )
```
![4](https://github.com/Vasuji/carnd-project1/blob/master/pipeline_images/4masked_image.jpg?raw=true)
#### Step-V:

In step V, I used ```houg_line``` helper function
```
 line_image = hough_lines(masked_image, rho =2, \
                          theta=np.pi/180,\
                          threshold=20, \
                          min_line_len=25,\
                          max_line_gap =10)
```
![5](https://github.com/Vasuji/carnd-project1/blob/master/pipeline_images/5line_image.jpg?raw=true)

#### Step-VI:

In step IV, I used
```

weighted_image = weighted_img(line_image, initial_img,
                           α=0.8,\
                           β=1.,\
                           λ=0.)
```
![6](https://github.com/Vasuji/carnd-project1/blob/master/pipeline_images/6weighted_image.jpg?raw=true)

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]





###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


###3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
