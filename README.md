# Empty space detection in Retail shelves where there is no product present.

### `Deepika Sharma`  ``||``                                      `Date : Aug 2020`

**These problems are seemingly difficult to solve and I've personally known/experienced such problems where it took 3 months time to get a reasonable solution :)**

## Notebook Structure
- Appraoches: 

- 1. OpenCV
- 2. YOLO
- 3. Mask RCNN
- 4. Custom appraoch : Suggested
- Challanges, Way Forward



### Actual Images

![alt text](https://github.com/Deepika-Sharma08/Object-detection-MRCNN-Yolo/blob/master/input_pngs.pngs?raw=true)

### Methodology Using OpenCV

`Steps taken to get the empty space as foreground`

1. Reading images as numpy array using opencv.
2. Histogram based thresholding to seperate foreground and background.
3. Canny edge detection to find objects in the image.
4. Dilate and erode image with vertical and horizontal kernals to merge edges if too close.
5. Reverse the image to get empty space highlighted as 1's.
6. Co-ordinates detection using rectangle identification [rectangles of ones in the image] 
