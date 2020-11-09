
**Advanced lane finding project**

The steps for this project are following:-

* Campute camera calibration matrix and distortion coefficient of the given set of chessboard images.
* Apply distortion correlation to the raw images.
* Apply color transformation, gradients, etc., to create thresholded binary images.
* Apply a perspective transformation to rectify binary image.("bird-eye-view")
* Detect lane pixel and fit to find the lane boundary.
* Determine curvature of lane and position of car with respect to the center.
* Warp detected lane boundaries back to the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.


[//]: # (Image References)

[image1]: ./examples/undistort_output.png "Undistorted"
[image2]: ./test_images/test1.jpg "Road Transformed"
[image3]: ./examples/binary_combo_example.jpg "Binary Example"
[image4]: ./examples/warped_straight_lines.jpg "Warp Example"
[image5]: ./examples/color_fit_lines.jpg "Fit Visual"
[image6]: ./examples/example_output.jpg "Output"
[video1]: ./project_video.mp4 "Video"


### Camera Calibration

The code for this step is contained in the third and fourth code cell of the IPython notebook located in "./advanced_lane_finding.ipynb".  

I start by preparing "object points", which will be the (x, y, z) coordinates of the chessboard corners in the world. Here I am assuming the chessboard is fixed on the (x, y) plane at z=0, such that the object points are the same for each calibration image.  Thus, `objp` is just a replicated array of coordinates, and `objpoints` will be appended with a copy of it every time I successfully detect all chessboard corners in a test image.  `imgpoints` will be appended with the (x, y) pixel position of each of the corners in the image plane with each successful chessboard detection.  

I then used the output `objpoints` and `imgpoints` to compute the camera calibration and distortion coefficients using the `cv2.calibrateCamera()` function.  I applied this distortion correction to the test image using the `cv2.undistort()` function and obtained this result: 

![alt text][image1]

### Pipeline (single images)

#### 1. Distortion-corrected image.

To demonstrate this step, I used undistort() method

#### 2. Color transforms, gradients or other methods to create a thresholded binary image.

I used a combination of color and gradient thresholds to generate a binary image in the lane_detector() method.

#### 3. Perspective transform

The code for my perspective transform includes a function called `warper()`, which appears in lines 1 through 8 in the file `example.py` (output_images/examples/example.py) (or, for example, in the 3rd code cell of the IPython notebook).  The `warper()` function takes as inputs an image (`img`), as well as source (`src`) and destination (`dst`) points.  I chose the hardcode the source and destination points in the following manner:

```python
src = np.float32([[800,510],[1150,700],[270,700],[510,510]])
    dst = np.float32([[650,470],[640,700],[270,700],[270,510]])
```


I verified that my perspective transform was working as expected by drawing the `src` and `dst` points onto a test image and its warped counterpart to verify that the lines appear parallel in the warped image.


#### 4. Identification of lane-line pixels and fit their positions with a polynomial

In the fit_lines() I found the left and right coefficients of lines and in method fit_continuous() used this coeffients to get the line pixel in subsequent frames.


#### 5. calculation the radius of curvature of the lane and the position of the vehicle with respect to center.

In the curavature() method I found the radii of curvature and center.
