# Yolov5_DeepSort_Pytorch_SpeedEstimate

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1RKw3VFzFPjO0UmDHHJlzGLZ8Eo6Fkv_4?usp=sharing)

Co-authored-by: allen-techguy <https://github.com/Allen-Hsiao>

Co-authored-by: Justin-TheGreat <https://github.com/Justin-TheGreat>






## Introduction

This repository contains a two-stage-tracker. The detections generated by [YOLOv5](https://github.com/ultralytics/yolov5), a family of object detection architectures. We utilized transfer learning to enhance the ability of vehicle recognition in Taiwan (Asia). The information is passed to a [Deep Sort algorithm](https://github.com/ZQPei/deep_sort_pytorch) which tracks the objects. The location information will then be calculated to decide whether it should send a warning signal to the driver. It can track any object that our Yolov5 model was trained to detect. This repository also gives you the freedom to use your own weights. 
Use your engineering judement to calibrate pixel_to_xy.py file.

## Tutorials

* [Yolov5 training on Custom Data (link to external repository)](https://github.com/ultralytics/yolov5/wiki/Train-Custom-Data)&nbsp;
* [Deep Sort deep descriptor training (link to external repository)](https://github.com/ZQPei/deep_sort_pytorch#training-the-re-id-model)&nbsp;


## You can use Google Colab to try out the code
## Before you run the tracker

1. Clone the repository recursively:

`!git clone --recurse-submodules https://github.com/Justin-TheGreat/Yolov5_DeepSort_Pytorch_SpeedEstimate.git`

If you already cloned and forgot to use `--recurse-submodules` you can run `git submodule update --init`

2. Make sure that you fulfill all the requirements: Python 3.8 or later with all [requirements.txt](https://github.com/mikel-brostrom/Yolov5_DeepSort_Pytorch/blob/master/requirements.txt) dependencies installed, including torch>=1.7. To install, run:

`%cd /content/Yolov5_DeepSort_Pytorch_SpeedEstimate`

`!pip install -r requirements.txt`
## Upload video and weight to Google Disk

```bash
# Upload the testing file
from google.colab import files
uploaded = files.upload()
```
## Upload video and weight to Google Drive and then copy it to the directory
You can download our pre-trained weight [here](https://drive.google.com/file/d/1s5sk_bnLpvAbBuREfKyoQ-T-ltA4g2um/view?usp=sharing).

```bash
from google.colab import drive
drive.mount('/content/drive')
```
```bash
%cp '/content/drive/Drive/XXXXXXXXXXXX' /content/Yolov5_DeepSort_Pytorch_SpeedEstimate # fill the "X" with the directory of the weight
```
```bash
%cp '/content/drive/MyDrive/XXXXXXXXXXXX' /content/Yolov5_DeepSort_Pytorch_SpeedEstimate # fill the "X" with the directory of the video
```
```bash

```

## Select a Yolov5 Pre-train weight
There is a clear trade-off between model inference speed and accuracy. In order to make it possible to fulfill your inference speed/accuracy needs
you can select a Yolov5 family model for automatic download

```bash
!python3 track.py --source XXX --yolo_weights Concern_free_turn_weight.pt --img 640 --save-vid # largest yolov5 family model
```
- Video:  `--source file.mp4`
- Webcam:  `--source 0`
- RTSP stream:  `--source rtsp://170.93.143.139/rtplive/470011e600ef003a004ee33696235daa`
- HTTP stream:  `--source http://wmccpinetop.axiscam.net/mjpg/video.mjpg`


## Filter tracked classes

By default the tracker tracks all MS COCO classes.

If you only want to track persons I recommend you to get [these weights](https://drive.google.com/file/d/1gglIwqxaH2iTvy6lZlXuAcMpd_U0GCUb/view?usp=sharing) for increased performance

```bash
!python3 track.py --source XXX --yolo_weights Concern_free_turn_weight.pt --classes 0 --save-vid # tracks persons, only
```

If you want to track a subset of the MS COCO classes, add their corresponding index after the classes flag

```bash
!python3 track.py --source XXX --yolo_weights Concern_free_turn_weight.pt --classes 16 17 --save-vid # tracks cats and dogs, only
```

[Here](https://tech.amikelive.com/node-718/what-object-categories-labels-are-in-coco-dataset/) is a list of all the possible objects that a Yolov5 model trained on MS COCO can detect. Notice that the indexing for the classes in this repo starts at zero.

You can find the result video under inference/output folder.

## Other information

For more detailed information about the algorithms and their corresponding lisences used in this project access their official github implementations.

