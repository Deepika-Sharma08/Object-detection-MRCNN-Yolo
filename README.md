# Empty space detection in Retail shelves where there is no product present.

### `Deepika Sharma`  ``||``                                      `Date : Aug 2020`

**These problems are seemingly difficult to solve and I've personally known/experienced such problems where it took 3 months time to get a reasonable solution :)**

** Note: This solution does not include training any Deep Learning model for detecting empty spaces in Retail shelves, instead I have put efforts in making use of functionalities of existing computer vision libraries and pre-trained models to validate if a solution can be build to handle this problem.


## Notebook Structure
- Approaches: 

- 1. OpenCV
- 2. YOLO
- 3. Mask RCNN
- 4. Custom approach : Suggested
- Challenges, Way Forward



### Actual Images

![alt text](https://github.com/Deepika-Sharma08/Object-detection-MRCNN-Yolo/blob/master/input_pngs.png?raw=true)

### Methodology Using OpenCV

`Steps taken to get the empty space`

1. Reading images as numpy array using opencv.
2. Histogram based thresholding to create binary image.
3. Canny edge detection to find edges/objects in the image.
4. Dilate and erode image with vertical and horizontal kernels to merge edges if too close.
5. Reverse the image to get empty space highlighted as 1's.
6. Co-ordinates detection using rectangle identification [rectangles of ones in the image] 


### Segmented Images

![alt text](https://github.com/Deepika-Sharma08/Object-detection-MRCNN-Yolo/blob/master/Results_/segmented_images.png?raw=true)


### Challenges using Open CV
- If in given image, products are placed behind each other then depth of the product is difficult to estimate using present algorithm and it is not able to pick if there is empty space in front of product which is placed in second row. It can be fixed using depth based filter.
- If there other objects in the image like floor, roof, human.. algorithms is failing to seperate the two using canny edge detection,,, which of course is not a right tool for seperating the objects.


`For separating objects, CascadeClassifier can be trained for various possible objects in the image for separating objects of interest vs other objects.`
- if product box contains black color logo which is very large or product box itself is black color, thresholding based approach tend to classify such objects as background. More adaptive ways to binarise the images is required.


### Other methods tried
1. YOLO
2. MaskRCNN

These methods are used to detect objects in retail shelves images and finding corresponding bboxes. Since OpenCV results do not provide any probability for identified blank spaces, output of Yolo and MaskRCNN is used to validate Opencv results if bboxes for identified blank spaces do not intersect with bboxes identified for objects using Yolo and MaskRCNN.

### Results look like this:

![alt text](https://github.com/Deepika-Sharma08/Object-detection-MRCNN-Yolo/blob/master/Results_/Results_using_Blob%20detection.png?raw=true)


### Closing Notes:
`To build a foolproof solution for this problem, I'll suggest transfer learning using VGG 16/19/UNet and only shallow training last few layers to achieve the objective.`

Which will require:


**a.** Annotated data which has bounding boxes for void/blank spaces where no product is placed.

**b.** Corresponding names of all possible classes under which shelf products can possibly fall.


` This information will be required for machine to automatically identify relative dimensions and specifications for blank/void space.`

**c.** Data across various departments for better generalisation.

### Related work:
I've built a similar solution for other project where objective was to detect `ALL` wheat heads in given images.
Annotated data contained 3000 images for training and ~300 images were left for testing. Following is the link for the solution:

https://github.com/Deepika-Sharma08/Wheat_head_prediction/blob/master/Wheat%20head%20detection%20VGG%20Unet%20Pyspark%20v1.html
