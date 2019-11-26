---
title: Advanced Lane Finding for Self-Driving Cars
summary:  Built advanced lane-finding algorithm using distortion correction, image rectification, color transforms, and gradient thresholding
tags:
- Autonomous Driving
- Computer Vision
- Pattern Recognition
- CNN
- Object Detection
date: "2019-06-11T00:00:00Z"
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
  caption: Lane detection for self-driving cars
  focal_point: Smart
  preview_only: false

url_code: "https://github.com/EricMFischer/self-driving-car-nano-degree/tree/master/advanced-lane-lines"
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

To perform lane finding for self-driving cars, we can outline some goals as the following:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.<br/>
* Apply the distortion correction to the raw image.<br/>
* Use color transforms, gradients, etc., to create a thresholded binary image. <br/>
* Apply a perspective transform to rectify binary image ("birds-eye view"). <br/>
* Detect lane pixels and fit to find lane boundary. <br/>
* Determine curvature of the lane and vehicle position with respect to center. <br/>
* Warp the detected lane boundaries back onto the original image. <br/>
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position. <br/>

First, we compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
{{< figure src="chessboard.png" lightbox="true" width="50%" height="50%" >}}

Second, we will run through our image pipeline, starting with our original image.
{{< figure src="original_image.png" lightbox="true" width="50%" height="50%" >}}

We need to apply a distortion correction to the raw image. Notice how the street sign is straight now.
{{< figure src="undistorted_image.png" lightbox="true" width="50%" height="50%" >}}

Then we use a color transforms, gradients, etc., to create a thresholded binary image.
{{< figure src="camera_calibration.png" lightbox="true" width="50%" height="50%" >}}

We obtain the lanes from the previous image and then apply a perspective transform to rectify binary image and create a "birds-eye" view.
{{< figure src="perspective_transform.png" lightbox="true" width="50%" height="50%" >}}

Now we can detect the lane pixels and fit to find the lane boundary.
{{< figure src="detect_lane.png" lightbox="true" width="50%" height="50%" >}}
{{< figure src="fill_lane.png" lightbox="true" width="50%" height="50%" >}}

With the lane boundary detected, we can determine curvature of the lane and vehicle position with respect to center and then warp the detected lane boundaries back onto the original image.

{{< figure src="road_with_lane.png" lightbox="true" width="50%" height="50%" >}}

On the image, we can output the visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

{{< figure src="final_result.png" lightbox="true" width="50%" height="50%" >}}
