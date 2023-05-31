# x
Drowsiness detection
reasons for importing libraries:
    1.from scipy.spatial import distance: This library is used to calculate the Euclidean distance between points in the eye landmarks, which is required for calculating the eye aspect ratio.

    2.from imutils import face_utils: The face_utils module from imutils provides convenient functions to work with facial landmarks, such as defining the indices for specific facial features like the left and right eye.

    3.from pygame import mixer: This library is used for playing audio files. In the code, it is specifically used to load and play the alert sound when drowsiness is detected.

    4.import imutils: The imutils library provides a set of utility functions to make working with OpenCV easier. In this code, it is used to resize the video frame, making the processing faster and more efficient.

    5.import dlib: Dlib is a powerful library for facial detection and facial landmark prediction. It is used in this code for detecting faces in the video frames and predicting the facial landmarks, which include the eye landmarks.

    6.import cv2: This is the OpenCV library, which is extensively used for computer vision tasks. It is used in this code for capturing video from the camera, processing frames, drawing contours, and displaying the final output.
    -----------
    The eye_aspect_ratio function calculates the eye aspect ratio (EAR) using the given eye landmarks. Here's an explanation of each step involved:

    A = distance.euclidean(eye[1], eye[5]): This line calculates the Euclidean distance between the second and sixth landmarks of the eye. These landmarks correspond to the vertical extent of the eye.

    B = distance.euclidean(eye[2], eye[4]): This line calculates the Euclidean distance between the third and fifth landmarks of the eye. These landmarks correspond to the horizontal extent of the eye.

    C = distance.euclidean(eye[0], eye[3]): This line calculates the Euclidean distance between the first and fourth landmarks of the eye. These landmarks correspond to the diagonal extent of the eye.

    ear = (A + B) / (2.0 * C): Finally, the eye aspect ratio is computed by dividing the sum of A and B by twice the value of C. The EAR is a measure of the eye's openness, where lower values indicate a more closed eye, potentially indicating drowsiness.
    ---------
    AFTER IMPORTING ALL THE LIB

    Initialize audio playback: The mixer module from pygame is initialized, and an alert sound is loaded using mixer.music.load().

Define the eye aspect ratio (EAR) function: The eye_aspect_ratio function calculates the EAR using Euclidean distances between eye landmarks.

Set threshold and frame check values: The thresh variable defines the threshold value for the EAR below which drowsiness is detected. The frame_check variable sets the number of consecutive frames the EAR must be below the threshold to trigger an alert.

Load face detection and landmark prediction models: The detect variable uses the dlib library to load a pre-trained face detection model. The predict variable loads a pre-trained facial landmark prediction model.

Define left and right eye indices: The (lStart, lEnd) and (rStart, rEnd) variables specify the indices for the left and right eye landmarks in the 68 facial landmarks.

Start video capture: The code creates a video capture object using cv2.VideoCapture(0) to access the default camera.

Initialize variables: The flag variable keeps track of consecutive frames where drowsiness is detected.

Start the main loop: The code enters a continuous loop to process each frame.

Read and preprocess the frame: The code reads a frame from the video capture and resizes it using imutils.resize(). The frame is converted to grayscale using cv2.cvtColor().

Detect faces and predict landmarks: The detect function detects faces in the grayscale frame. For each face, the facial landmarks are predicted using the predict function.

Calculate eye aspect ratio and draw eye contours: The EAR is calculated for each eye using the eye_aspect_ratio function. The contours of the eyes are drawn on the frame using cv2.drawContours().

Check for drowsiness: If the EAR is below the threshold, the flag counter is incremented. If the flag exceeds the frame check value, an alert message is drawn on the frame and the alert sound is played.

Reset the counter: If the EAR is above the threshold, the flag counter is reset to 0.

Display the frame: The frame with eye contours and alert message is displayed using cv2.imshow().

Check for key press and exit: The code waits for a key press and checks if it is the 'q' key. If 'q' is pressed, the loop is exited.

Clean up resources: Finally, the windows are closed and the video capture is released using cv2.destroyAllWindows() and cap.release().