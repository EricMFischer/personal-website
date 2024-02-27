---
title: Topology Adaptive Snakes Improve Mask Generation for Image Inpainting
summary: T-snake deformable models, which can segment complex-shaped structures, improve generated masks passed to GAN for image inpainting
tags:
- Computer Vision
- Deformable Model
- Topology Adaptive Snakes
- Generative Modeling
- Image Inpainting
- CNN
- Image Segmentation
date: "2019-06-03T00:00:00Z"
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
  caption: Image inpainting
  focal_point: Smart
  preview_only: true

url_code: "https://github.com/CS269-Capstone/t-snake-mask-generation"
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

Image inpainting is the process of reconstructing lost or deteriorated parts of an image. Yu et al. provide a generative image inpainting system which is able to inpaint images that have had portions manually erased by a user.
Unlike other state-of-the-art inpainting techniques, which erase regions covered by rectangular masks, their proposed system allows a user to erase arbitrarily-shaped portions of an image by `drawing' a free-form mask directly onto the image.

Additionally, this mask can be composed of multiple disjoint regions. The Yu et al. paper provides a generative image inpainting system which is able to operate on images with free-form masks, a key differentiator from many other state of the art inpainting techniques which require rectangular masked regions. It can do this by implementing a so-called SN-PatchGAN, a Generative Adversarial Network loss function which is patch-based, as opposed to using a traditional rectangular mask.

One problem not directly addressed by the paper is that of generating the masks. The system developed by Yu et al. requires the user to manually “erase” the object to be painted over. Unless the user takes extreme care in outlining the object, the resulting mask will likely erase more of the image than intended, thereby removing potentially valuable information that the inpainting algorithm could have otherwise used to produce a more believable result. We can see an example of a manual masking of people in a museum where significant portions of the background are erased inadvertently.

{{< figure src="statue.png" lightbox="true" width="80%" height="80%" >}}

Given that SN-PatchGAN relies on convolutional filters to perform the inpainting, this loss of spatially local information could have noticeable effects on the quality of the output image. The goal of this paper, then, was to find a method that can neatly outline the object to be erased, avoiding the loss of information from inaccurate manual masking.

The topic of generating masks is solved exceptionally well by many different variations of active contour models (also known as snakes). Specifically, we will look to extend the use of topology adaptive snakes, i.e. T-snakes.

We extend the functionality of the Yu et al. paper by using a deformable model to accurately extract the object to be removed.
After the user (broadly) erases the object to be inpainted, we extract the erased portion of the image (the `hole'), a non-rectangular subset of the original image. Using a topology adaptive snake model that demonstrates “shrink-wrap” behavior, we form a closed mask which follows the desired object much more closely.

The updated mask is then be passed to the SN-PatchGAN to produce a more realistic inpainted image. In this way, we minimize the amount of erasure/modification that the GAN does to the original image. For visualization, the proess of passing the mask to the GAN is outlined below.

First, we load and display the grayscale image and raw input mask.

{{< figure src="1.png" lightbox="true" width="70%" height="70%" >}}

Then we compute the bounding boxes for each distinct masked region.

{{< figure src="2.png" lightbox="true" width="70%" height="70%" >}}

Lastly, we dislay the sub-images that will each be processed separately.

{{< figure src="3.png" lightbox="true" width="70%" height="70%" >}}
{{< figure src="4.png" lightbox="true" width="70%" height="70%" >}}
{{< figure src="5.png" lightbox="true" width="70%" height="70%" >}}

Taken from the original T-snakes paper, here is a diagram giving an idea of the logic behind the T-snake deformable model.

{{< figure src="t-snake-diagram.png" lightbox="true">}}

Here is a topology adaptive snake being applied to a similar problem: filling a region inside the human brain.

{{< figure src="featured.png" lightbox="true" width="30%" height="30%" >}}

