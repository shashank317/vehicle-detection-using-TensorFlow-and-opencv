This project is a solid foundation for building an autonomous vehicle vision system. It tackles the critical challenge of detecting vehicles on the road using TensorFlow and OpenCV.

Here’s a breakdown of the project and its capabilities:

## What It Does

The script performs real-time detection of vehicles (like cars, trucks, and buses) in a video stream. It uses the YOLO (You Only Look Once) object detection model, specifically a trained version for vehicle detection.

The system can:

*   **Load a Pre-trained Model**: It initializes a `vehicles_yolo_model_v5` using TensorFlow, which is ready to detect vehicles.
*   **Read Video**: It reads frames sequentially from a video file (`vehicle.mp4`).
*   **Detect Objects**: For each frame, it identifies vehicles using the YOLO model.
*   **Draw Bounding Boxes**: It draws colorful boxes around each detected vehicle and labels them with the class name and confidence score (e.g., "car 91%").
*   **Track Vehicles**: The `count_vehicle` function tracks vehicles across frames, ensuring that if the same vehicle appears in multiple consecutive frames, it’s counted only once.
*   **Display Count**: It shows the running count of vehicles detected so far on the top-left corner of the output video.

## How It Works

The core logic is implemented in the `vehicle_detection` function:

1.  **Initialization**: It loads the YOLO model (`vehicle.tflite`) and sets up the video capture.
2.  **Inference Loop**: It iterates through the video frames:
    *   Resizes the frame to the model's input size (640x640).
    *   Normalizes pixel values to the range [-1, 1], which is required for this model.
    *   Feeds the processed frame into the YOLO model to get predictions (boxes, scores, classes).
3.  **Post-Processing**: It filters the raw model outputs to identify valid vehicle detections and draws them on the frame.
4.  **Counting**: It uses a simple frame-skipping logic and a tracking dictionary to count distinct vehicles.
5.  **Output**: It saves the annotated video to `vehicle_output.mp4`.

## How to Run It

1.  **Prerequisites**: Ensure you have Python installed along with the necessary libraries:
    ```bash
    pip install tensorflow opencv-python numpy
    ```

2.  **Model**: Make sure the pre-trained model `vehicle.tflite` is in the same directory as the script, or update the `MODEL_PATH` variable in the script to point to its location.

3.  **Run the script**:
    ```bash
    python vehicle_detection.py
    ```

The script will process the `vehicle.mp4` video and save the result as `vehicle_output.mp4`.
    