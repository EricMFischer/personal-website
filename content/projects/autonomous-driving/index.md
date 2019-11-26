---
title: Car Detection for Autonomous Driving
summary: Achieving high-accuracy in real-time, YOLO algorithm is applied to car detection for autonomous vehicles
tags:
- Autonomous Driving
- Computer Vision
- Pattern Recognition
- CNN
- Object Detection
- YOLO Algorithm
- Non-Maximum Suppression
date: "2018-08-10T00:00:00Z"
# featured: true

# Optional external URL for project (replaces project detail page).
external_link: ""

# Featured image
# To use, place an image named `featured.jpg/png` in your page's folder.
# Placement options: 1 = Full column width, 2 = Out-set, 3 = Screen-width
# Focal point options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
# Set `preview_only` to `true` to just use the image for thumbnails.
image:
  placement: 1
  caption: Car detection for autonomous vehicles
  focal_point: Smarts
  preview_only: true

url_code: "https://github.com/EricMFischer/deep-learning-specialization/blob/master/convolutional-neural-networks/week-3/autonomous-driving-car-detection/Autonomous%20driving%20application%20-%20Car%20detection%20-%20v1.ipynb"
url_pdf: ""
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
# slides: example
---

Let us take a look at object detection using the very powerful YOLO model. Many of the ideas here are described in the two YOLO papers: Redmon et al., 2016 (https://arxiv.org/abs/1506.02640) and Redmon and Farhadi, 2016 (https://arxiv.org/abs/1612.08242).

YOLO ("you only look once") is a popular algoritm because it achieves high accuracy while also being able to run in real-time. This algorithm "only looks once" at the image in the sense that it requires only one forward propagation pass through the network to make predictions. After non-max suppression, it then outputs recognized objects together with the bounding boxes.

Here's one way to visualize what YOLO is predicting on an image. For each of the 19x19 grid cells, we can find the maximum of the probability scores (taking a max across both the 5 anchor boxes and across different classes). I we color that grid cell according to what object the grid cell considers the most likely, we get the following result.

{{< figure src="yolo_image.png" lightbox="true" width="50%" height="50%" >}}

Note that this visualization isn't a core part of the YOLO algorithm itself for making predictions; it's just a nice way of visualizing an intermediate result of the algorithm.

Another way to visualize YOLO's output is to plot the bounding boxes that it outputs. Doing that results in a visualization like this.

{{< figure src="yolo_box_image.png" lightbox="true" width="40%" height="40%" >}}

In the figure above though, we plotted only boxes that the model had assigned a high probability to and this is still too many boxes. We'd like to filter the algorithm's output down to a much smaller number of detected objects. To do so, we'll use non-max suppression. Specifically, we'll carry out these steps:

* Get rid of boxes with a low score, i.e. box is not very confident about detecting a class
* Select only one box when several boxes overlap with each other and detect the same object

Even after filtering by thresholding over the classes scores, we still end up a lot of overlapping boxes. A second filter for selecting the right boxes is called non-maximum suppression (NMS).

{{< figure src="before_nms.png" lightbox="true" width="40%" height="40%" >}}
{{< figure src="after_nms.png" lightbox="true" width="40%" height="40%" >}}

Applying the YOLO model to a hold-out image, an example result is the following.

{{< figure src="featured.png" lightbox="true" width="50%" height="50%" >}}
