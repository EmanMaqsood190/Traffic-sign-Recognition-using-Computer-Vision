
# Traffic Sign Recognition System using Computer Vision

An intelligent, rule-based Computer Vision system designed to detect and categorize traffic signs from images using **HSV color segmentation** and **geometric contour analysis**. 

Unlike deep learning approaches that require heavy computational resources and massive datasets, this project leverages traditional image processing techniques with `OpenCV` to isolate specific color spaces, approximate geometric shapes, and classify signs instantly.

#  Features

 **Color Space Segmentation:** Converts source images into the HSV (Hue, Saturation, Value) color space for resilient color extraction under varying light conditions.
 **Multi-Color Masking:** Implements customized threshold masks for **Red**, **Blue**, **Yellow**, and **White** color ranges.
 **Morphological Refinement:** Applies closing operations (`cv2.MORPH_CLOSE`) to eliminate background noise, fill gaps, and smooth detection boundaries.
 **Geometric Classification:** Automatically approximates contour shapes and counts vertices to differentiate between circular, triangular, octagonal, rectangular, and diamond-shaped signs.
 **Dynamic Annotation:** Draws bounding boxes and places descriptive labels cleanly above each identified sign.



#  How It Works (The Classification Pipeline)

The core logic analyzes two key properties of each detected region: **Color Dominance** (pixel counts per mask) and **Geometry** (vertex approximation via `cv2.approxPolyDP`).

 Input Image ➔  HSV Conversion ➔  Color Masks ➔  Morphological Cleaning ➔  Shape Analysis ➔  Annotated Output
## Yellow Dominance:

4 Vertices (Diamond): Classified as U-TURN signs.

Other Shapes: Classified as general CAUTION signs.

## Red Dominance:

Many Vertices (>5) + High White Content: Classified as SPEED LIMIT signs.

High Vertices (>5) + Low White Content: Classified as STOP signs.

3 to 4 Vertices (Triangles/Rectangles): Classified as DANGER / WARNING signs.

## Blue Dominance:

4 Vertices (Perfect Rectangles/Squares): Classified as PARKING signs.

Circular/Other Shapes: Classified as DIRECTIONAL signs.

## Project Structure
 ├── Traffic_signs_recognation.ipynb  # Main Jupyter Notebook / Google Colab Pipeline
├── traffic signs.jpg                # Sample testing dataset image
└── README.md                        # Project documentation

# Installation & Setup
Clone the Repository:
git clone [https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git](https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git)
cd YOUR_REPO_NAME

Install Required Libraries:
Make sure you have Python installed, then run:
pip install opencv-python-headless matplotlib numpy

Run the Project:
Open the Jupyter Notebook (Traffic_signs_recognation.ipynb) in your preferred environment (VS Code, Jupyter Lab, or upload it directly to Google Colab) and run all cells sequentially.

 # Current Limitations
1.While traditional computer vision algorithms are incredibly fast and lightweight, they have explicit operational thresholds:

2.Strict Color Thresholds: Radical environmental changes (e.g., night-time driving, heavy shadows, directly glaring sunlight, or lens flares) can shift the HSV values, leading to missed detections.

3.Angle and Distortion Sensitivity: Geometric vertex approximation (approxPolyDP) relies on clear structural profiles. If a sign is bent, heavily rotated, or viewed from a sharp side angle, the vertex count might misclassify the shape.

4.Overlapping Backgrounds: If objects in the environment (like red brick buildings, yellow cars, or blue billboards) fall within the targeted HSV thresholds and sit near structural shapes, the algorithm can produce false positives.

 # Future Improvements
1.To transform this lightweight system into a highly robust, production-grade application, the following updates are planned:

2. Adaptive Thresholding: Integrate dynamic illumination adjustment algorithms to automatically alter HSV ranges based on global image brightness levels.

3. Temporal Consistency (Video Stream Tracking): Implement a tracking filter (like a Kalman Filter or Centroid Tracker) to carry over bounding boxes across sequential video frames, smoothing out sporadic single-frame misses.

4. Hybrid Deep Learning Framework: Introduce a lightweight neural network (like MobileNetV3 or a custom shallow CNN) acting exclusively as a secondary validation stage to read numbers inside SPEED LIMIT signs and verify labels.

5. Region of Interest (ROI) Filtering: Add structural constraints to filter out detections that don't match standard aspect ratios of realistic traffic signs, significantly reducing false-positive rates from background clutter.

 # License
This project is open-source and available under the MIT License. Feel free to modify, distribute, and build upon it!
