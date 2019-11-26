---
title: Vehicle Detection for Self-Driving Cars
summary: Created vehicle detection and tracking pipeline with OpenCV, histogram of oriented gradients, and SVM, and also with a deep network
tags:
- Autonomous Driving
- Computer Vision
- Pattern Recognition
- Image Gradients
- Object Detection
- Non-Maximum Suppression
- Histogram of Oriented Gradients
- SVM
date: "2019-06-10T00:00:00Z"
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
  caption: Vehicle detection for Self-Driving Cars
  focal_point: Smart
  preview_only: false

url_code: "https://github.com/EricMFischer/self-driving-car-nano-degree/tree/master/vehicle-detection"
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

The objective of this project is to create a pipeline (model) to draw bounding boxes around cars in a video. Example images and video come from a combination of the GTI vehicle image database and the KITTI vision benchmark suite. We have the following goals:

* Perform a Histogram of Oriented Gradients (HOG) feature extraction on a labeled training set of images and train a classifier Linear SVM classifier
* Implement a sliding-window technique and use trained classifier to search for vehicles in images
* Run pipeline on a video stream and create a heat map of recurring detections frame by frame to reject outliers and follow detected vehicles
* Estimate a bounding box for vehicles detected

First we perform a Histogram of Oriented Gradients (HOG) feature extraction on a labeled training set of images.

Here are examples of images from the vehicle class and the non-vehicle class.
{{< figure src="vehicle_hog.png" lightbox="true" width="70%" height="70%" >}}

Here are some visualized HOG features extracted from the images.
{{< figure src="hog_descriptors.png" lightbox="true" width="80%" height="80%" >}}

We can implement a sliding-window technique and use our trained classifier to find vehicles in images.
{{< figure src="hog_pipeline.png" lightbox="true" width="60%" height="60%" >}}

Initially using HOG features and SVM, a heatmap could average the detection results from successive frames. The heatmap was thresholded to a minimum value before labeling regions, to remove false positive. This process was shown above.

With deep learning, however, we can rely on a confidence score to decide the tradeoff between precision and recall. This next figure shows the effect of thresholding SSD detection at different level of confidence.

{{< figure src="bounding_boxes.png" lightbox="true" width="90%" height="90%" >}}
