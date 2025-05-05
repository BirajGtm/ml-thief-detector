# Thief Detector

## This shows Image Processing abilities to build a motion detection algorithm that alarms you when you have an unwanted visitor in camera frame.

## What it does

-   1.  Get the live video feed from your webcam
-   2.  Fix a scene (the place you want to monitor) and store it as a reference background image
    -   Store the first frame as the reference background frame
-   3.  For every frame, check if there is any unwanted object inside the scene you are monitoring
    -   Use **Background Subtraction** concept (**cv2.absdiff( )**)
        -   Subtract the current frame from the reference background image(frame) to see the changes in the scene
        -   If there is enormous amount of pixels distrubed in the subtraction result image
            -   unwanted visitor (place is unsafe --\> alarm the authorities)
        -   If there is no enormous amount of pixels distrubed in the subtraction result image
            -   no unwanted visitor (place is safe)
-   4.  Output the text **"UNSAFE"** in **red** color on the top right of the frame when there is an intruder in the scene.
-   5.  Save the live feed

## Dependencies

* OpenCV (`cv2`)
* time

## Installation

1.  Install the required packages:

    ```bash
    pip install opencv-python
    ```

2.  Clone this repository.

## Usage

1.  Run the `Thief_Detector.ipynb` notebook.
2.  The script will capture video from your default webcam.
3.  It will display a window showing the video feed with "UNSAFE" text when motion is detected.
4.  The video feed will also be saved to a file named `thief_detector_output.avi`.
5.  Press 'q' to quit.

## Code Description

### `get_video_capture()`

Initializes and returns the video capture object from the webcam.

### `get_reference_background(cap)`

Captures the initial background frame from the video feed, converts it to grayscale, and applies Gaussian blur for noise reduction.

### `compute_difference(frame, reference_gray)`

Computes the absolute difference between the current frame and the reference background frame.

### `apply_threshold(diff)`

Applies a threshold to the difference image to create a binary image highlighting motion.

### `find_motion_contours(thresh)`

Finds the contours (boundaries of moving objects) in the thresholded image.

### `mark_intrusion(frame, contours)`

Draws a rectangle around detected motion and adds "UNSAFE" text to the frame if significant motion is detected.

### `display_and_save(frame, out)`

Displays the processed frame and saves it to a video file.  It also checks for the 'q' key to quit.

### `release_all(cap, out)`

Releases the video capture and writer objects, and closes all windows.

### `run_thief_detector()`

Main function that runs the motion detection process.
