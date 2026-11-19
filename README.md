# AI Video Object Tracking - Cumulative Counting

Counts vehicles and people in a video using YOLOv8 detection and tracking. Each tracked object is counted once, by class, and the running totals are shown on each frame and written to an output video.

## Features

- YOLOv8 object detection and tracking via Ultralytics (`model.track`, persistent IDs)
- Counts each unique track ID once, per COCO class
- Class label smoothing over the last 5 frames to stabilize class names
- Draws boxes, IDs and running counts on every frame
- Writes the annotated result to an MP4 file

## Project structure

- `commulative_counting.py` - the main script. Loads `yolov8n.pt`, tracks objects in a video, counts them and saves the annotated output.
- `yolov8n.pt` - YOLOv8 nano weights (used by the script).
- `yolov8m.pt` - YOLOv8 medium weights (not referenced by the script; included as an alternative).
- Video files (`aaaa.mp4`, `car.mp4`, `carrss.mp4`, `DEMO_VIDEO.mp4`, `c_demo.mp4`, `car_demo.mp4`, `carrss_demo.mp4`, `d_demo.mp4`) - sample input and demo videos.

## Requirements

Python packages imported by the script:

- `ultralytics` (YOLOv8)
- `opencv-python` (imported as `cv2`)
- `numpy`

Install:

```
pip install ultralytics opencv-python numpy
```

## Installation

1. Clone the repository.
2. Install the packages above.
3. Make sure `yolov8n.pt` is in the same folder as the script (it is included).

## Usage

```
python commulative_counting.py
```

The script has no command-line arguments. Input and output paths are set in the file:

- `video_path` - the input video. It is currently a hard-coded Windows path to `aaa.mp4`; change it to one of the included videos (for example `car.mp4`).
- `output_path` - the output video, also a hard-coded path. Change it to a writable location such as `output.mp4`.

Frames are not shown in a window (`cv2.imshow` is commented out). Progress is saved to the output file, and the script prints the output path when it finishes. Press nothing; the run ends when the video ends.

## Notes

- The counting uses COCO class names for all 80 classes; the counts are shown per class for every object the detector tracks, not just vehicles and people.
- Detection confidence threshold is 0.5.
- Video paths and the output path are hard-coded from the original Colab/PyCharm setup and must be edited before running.
- The script was originally a Colab notebook export; the Colab-specific lines are commented out.
- The `yolov8m.pt` file is included but not used by the current code. Change `YOLO("yolov8n.pt")` to use it (slower, usually more accurate).
- Demo videos are included in the repo, and the file sizes may make cloning slower.
