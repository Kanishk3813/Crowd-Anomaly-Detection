# Crowd-Analysis

The project is dedicated to apply on CCTV and other survailance system for simple crowd monitoring and crowd analysis. The system is able to monitor for abnormal crowd activity, social distance violation and restricted entry. The other part of the system can then process crowd movement data into optical flow, heatmap and energy graph.

Abnormal crowd activity is monitored by computing crowd movement energy level.

Social distace violation is simply calculating distance between individuals. Two modes are given to calculate distance from edge of individuals or center of individuals from camera at different scenario.

Human detection is implemented using YOLOv4 via OpenCV built-in function. Tracking algorithm is implemented using Deep SORT

Current functions implemented includes:

- Social distance rule violation
- Entries to restriced areas
- Abnormal crowd movement/activity
- Crowd movement tracks and flow
- Crowd stationaries point (Heatmap)

---

**I am happy to talk about the project if you have any question or discussion!**

---

## Building

YOLOv4-tiny is used for this documentation. You can use other YOLO variation for desire usage and output.

### Files

Clone this repo. Then, create a folder ```YOLOv4-tiny```, download and put in the weight and config file. The files can be found here, [yolov4-tiny.weights](https://github.com/AlexeyAB/darknet/releases/download/darknet_yolo_v4_pre/yolov4-tiny.weights) and [yolov4-tiny.cfg](https://github.com/AlexeyAB/darknet/blob/master/cfg/yolov4-tiny.cfg).

### Requirements

Install the requirements

```shell
pip3 install requirements.txt
```

## Configuration

`config.py` contains all configurations for this program.

Place the **video source** under `VIDEO_CONFIG.VIDEO_CAP` in `config.py`

## Running

Before you run the program, make sure you have input a valid **video source**. You have to provide your own video for the program. Replace the path at `VIDEO_CONFIG.VIDEO_CAP` in `config.py` with the path of your own video.

To process a video, run `main.py`

```shell
python3 main.py
```

`main.py` will yield a set of data from the video source in the form of csv and json. These data will be placed in the directory `processed_data`.

From these data, you can generate movement data, crowd summary and abnormal crowd movement.

```shell
python3 abnormal_data_process.py
python3 crowd_data_present.py
python3 movement_data_present.py
```

`abnormal_data_process.py` will yield a summary for the processed energy data set and a graph of energy level over count. This process will clean outlier if the data set has a skewness larger than 7.5

`crowd_data_present.py` will yield a heatmap and optical flow. Optical flow shows the tracks of each individual. Heatmap shows the spot where individuals stop; the stronger the color, the longer or more individual stop at the given spot.

`movement_data_present.py` will yield a summary plot of crowd count, violation count, restricted entry detection and abnormal activity over time(frames).

## Sample Output

![Crowd Anomaly](https://github.com/Kanishk3813/Crowd-Anomaly-Detection/blob/main/processed_data/Crowd%20Anomaly.png)
