# **Finding Lane Lines on the Road** 


---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:

* Make a pipeline that finds lane lines on the road

* Reflect on your work in a written report


[image1]: ./test_images/solidWhiteRight.jpg
[image2]: ./test_images/solidYellowLeft.jpg


---------------------------------------------------------------------------------------------------------
Pipeline Description

My pipeline consisted of 5 steps: 

First, I converted the images to grayscale (step 1 : picture bellow on the 3)), 

then I define the kernel size and the gaussian smoothing (step2 : picture bellow on the 3)),

After that I define the parameters for Canny functions to obtain my edges in the image space (stage3: picture bellow on the 3)),

The next stage is the definition of the polygon to mask avd visualize only the content of the polygon (stage 4 : picture bellow on the 3)),

Then, we run the hough transform on the edge detected line segment with the hough parameters (Step 5 : picture bellow on the 3)),

Finally, we draw on the line on the image before the procesins (Step 6 : picture bellow on the 3).

---------------------------------------------------------------------------------------------------------
Draw continuous lines

In order to draw a single line on the left and right lanes, I modified the draw_lines() function.

-Initialization:

I use the fonction y= mx+b from the lecture with 4 empties list : 

  - 2 lists for the left line (initialization) : m>0  and bleft for the left line, 
  
  - 2 lists for the right line (initialization) : m<0 and bright for the right line.
  
- For every segment (for loop) :
    - I calculate the slop m and the intersection b with the y axis (from the equation y =bx+m)
    
    - if m>0 : I add the element m and bleft respectively in the lists mpositive and leftline
    
    - if m<=0 : I add the element m and bright respectively in the lists mnegative and rightline
    
- The lists are now completed and after the average of the 4 lists with the calculation x =(y - average(b))/(average(m)) and the y coordinate (bottom and top of the selected area), I can deduce :

    - for the left line :  the coordinate (xstart, ytart) and (xend,yend)
    
    - for the righ line :  the coordinate (xstart, ytart) and (xend,yend)

- The last step is to implement this 2 lines (right and left) on the picture with he fonction cv2.line

----------------------------------------------------------------------------------------------------

1) Draw_Lines function without modification

[Step 1]: ./test_images_output/Draw_Lines_initial/Grayscale_image_step1.jpg 
[Step 2]: ./test_images_output/Draw_Lines_initial/Gaussian_Kernel_step2.jpg
[Step 3]: ./test_images_output/Draw_Lines_initial/Canny_step3.jpg
[Step 4]: ./test_images_output/Draw_Lines_initial/Region_Interest_step4.jpg
[Step 5]: ./test_images_output/Draw_Lines_initial/Hough_step5.jpg
[Final]: ./test_images_output/Draw_Lines_initial/Final_Result_step6.jpg


2) Draw_Lines function with modification

[Step 1]: ./test_images_output/Draw_Lines_modified/Grayscale_image_step1.jpg 
[Step 2]: ./test_images_output/Draw_Lines_modified/Gaussian_Kernel_step2.jpg
[Step 3]: ./test_images_output/Draw_Lines_modified/Canny_step3.jpg
[Step 4]: ./test_images_output/Draw_Lines_modified/Region_Interest_step4.jpg
[Step 5]: ./test_images_output/Draw_Lines_modified/Hough_step5.jpg
[Final]: ./test_images_output/Draw_Lines_modified/Final_Result_step6.jpg


--------------------------------------------------------------------------------
CONCLUSION

I can sometimes and only temporary detect segment near the road (on the left in "solidYellowLeft"), it's a small line border beetween the road and the gap on the center, 

On the top of the interested area, I have systematiquely temporary short perturbation. The Canny threshold and the Hough parameters must be improved to delete totally these perturbations. 
 
A possible improvement would be to tune better the hyperparameters of the hough transform on the edges from the canny function. 
You can see always little undesirable segment (temporary) in the last video (yellowsolid). 

These Hough parameters  (in my case) are more the results of a series of trial and not theoritical (empirics methods). 




