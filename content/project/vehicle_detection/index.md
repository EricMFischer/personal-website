---
title: Vehicle Detection for Self-Driving Cars
summary: Image pipeline model for drawing bounding boxes around cars in a video
tags:
- Autonomous Driving
- Computer Vision
- Pattern Recognition
- CNN
- Image Gradients
- Object Detection
- Non-Maximum Suppression
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
  caption: Vehicle Detection for Self-Driving Cars
  focal_point: Smart
  preview_only: true

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
* Run pipeline on a video stream and create a heat map of recurring detections frame by frame to reject outliers and follow detected vehicles.
* Estimate a bounding box for vehicles detected.

First we perform a Histogram of Oriented Gradients (HOG) feature extraction on a labeled training set of images, and then we subsequently train a Linear SVM classifier using selected HOG features and colour features.

Here are two example images, the first from the vehicle class and the second from the non-vehicle class.
{{< figure src="for_hog.png" lightbox="true" width="25%" height="25%" >}}
Here are some visualized HOG features extracted from the images.
{{< figure src="hog.png" lightbox="true" width="35%" height="50%" >}}

Lastly, we can implement a sliding-window technique and use our trained classifier to find vehicles in images.
{{< figure src="featured.png" lightbox="true" width="60%" height="60%" >}}

