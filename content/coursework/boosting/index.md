---
title: Face Detection using AdaBoosting and RealBoosting
summary: If we can predict correctly at least 50% of the time
tags:
- Boosting
- AdaBoosting
- RealBoosting
- Haar Filter
- Pattern Recognition
- Computer Vision
date: "2018-10-20T00:00:00Z"
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
  caption: Haar filters
  focal_point: Smart
  preview_only: true

# links:
# - icon: github
#   icon_pack: fab
#   name: Follow
#   url: https://github.com/ericmfischer
url_code: "https://github.com/EricMFischer/adaboosting-realboosting-face-recog"
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

Boosting is a general method for improving the accuracy of any given learning algorithm. Specifically, one can use it to combine weak learners, each performing only slightly better than random guess, to form an arbitrarily good hypothesis.

First, for the weak classifiers $h$, we load the predefined set of Haar filters. We compute the features $f$ by applying each Haar filter to the integral images of the positive and negative populations. We determine the polarity $s$ and threshold $θ$ for each weak classifier $h$:

    h(x) = −s if f < θ
            s otherwise

Then we write a function which returns the weak classifier with lowest weighted error. Note, as the samples change their weights over time, the histograms and threshold $θ$ will change.

The AdaBoost algorithm boosts the weak classifiers. We construct the strong classifier $H(x)$ as an weighted ensemble of $T$ weak classifiers and run it on these images. We perform non-maximum suppression, i.e. when two positive detections overlap significantly, we choose the one that has higher score.

We perform hard negatives mining. Given a background image without faces, we run our strong classifier on these images. Any “faces” detected by our classifier are called “hard negatives”, and we add them to the negative population in the training set and re-train our model.

We can display the top 20 Haar filters after boosting, in order of their addition to the strong classifier $H(x)$. The activation of a Haar filter is equal to the sum of pixel values “underneath” white rectangles minus the sum “underneath” black rectangles. The boundary between dark and light regions in the Haar filters represent common dark to light transitions in actual images. For example, in human faces the eye region is darker than the upper cheeks, and the nose bridge region is brighter than the eyes, as represented by some of the Haar filters below.

{{< figure src="featured.png" lightbox="true" width="50%" height="50%" >}}

At steps $T = 0, 10, 50, 100$, we can plot the curve for the training errors of the top $1000$ weak classifiers among the pool of weak classifiers in increasing order. The top $1000$ weak classifier accuracies converge to $0.5$ as more weak classifiers are selected to be added to the strong classifier. After $100$ selections, accuracy and hence error are very near $0.5$.

{{< figure src="wc_accuracies.png" lightbox="true" width="60%" height="60%" >}}

For non-maximum suppression, when the ratio of overlap (which is computed with areas) between positive detections is more than $0.01$, the positive detections with higher scores (i.e. greater probabilities of being a face) are preferred and kept and others are removed. Increasing the overlap threshold to be more than $0.01$ would cause there to be even less positive detections after applying NMS. We expect there to be significantly less false positive detections of faces after training a Boosting model with a considerable amount of hard negative image patches added to the non-face dataset.

{{< figure src="face_detection.png" lightbox="true" width="55%" height="55%" >}}


