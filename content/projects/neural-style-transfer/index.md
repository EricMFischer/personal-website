---
title: Neural Style Transfer using Convolutional Neural Networks
summary: Neural style transfer generates images that reflect the content of one image but the artistic "style" of another
tags:
- Image Style Transfer
- CNN
- Pattern Recognition
- Computer Vision
date: "2019-04-12T00:00:00Z"
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
  caption: An example of image style transfer
  focal_point: Smart
  preview_only: true

url_code: "https://github.com/EricMFischer/CS231n/blob/master/assignment3/StyleTransfer-TensorFlow.ipynb"
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

We take a look at the style transfer technique from "Image Style Transfer Using Convolutional Neural Networks" (Gatys et al., CVPR 2015). The general idea is to take two images, and produce a new image that reflects the content of one but the artistic "style" of the other. We will do this by first formulating a loss function that matches the content and style of each respective image in the feature space of a deep network, and then performing gradient descent on the pixels of the image itself. The deep network we use as a feature extractor is SqueezeNet, a small model that has been trained on ImageNet. You could use any network, but we chose SqueezeNet here for its small size and efficiency. Here's an example of what we'll be able to produce, a real image with the style of a work of art:

{{< figure src="example.png" lightbox="true" width="50%" height="50%" >}}

After building loss functions for the content loss, style loss, and total variation loss, I was able to generate some images.

First, what is the content loss function? We can generate an image that reflects the content of one image and the style of another by incorporating both in our loss function. We want to penalize deviations from the content of the content image and deviations from the style of the style image. We can then use this hybrid loss function to perform gradient descent not on the parameters of the model, but instead on the pixel values of our original image. So content loss measures how much the feature map of the generated image differs from the feature map of the source image. We only care about the content representation one layer of the network when considering the content loss.

Now what is the style loss? For a given layer $\ell$, the style loss is defined as follows. First, we compute the Gram matrix G which represents the correlations between the responses of each filter, where F is as above. The Gram matrix is an approximation to the covariance matrix -- we want the activation statistics of our generated image to match the activation statistics of our style image, and matching the (approximate) covariance is one way to do that. There are a variety of ways you could do this, but the Gram matrix is nice because it's easy to compute and in practice shows good results. Assuming $G^{\ell}$ is the Gram matrix from the feature map of the current image, $A^{\ell}$ is the Gram Matrix from the feature map of the source style image, and $w_{\ell}$ a scalar weight term, then the style loss for the layer ${\ell}$ is simply the weighted Euclidean distance between the two Gram matrices.

What is the total variation loss? Well, it turns out that it's helpful to also encourage smoothness in the image. We can do this by adding another term to our loss that penalizes wiggles or "total variation" in the pixel values. You can compute the "total variation" as the sum of the squares of differences in the pixel values for all pairs of pixels that are next to each other (horizontally or vertically). Here we sum the total-variation regualarization for each of the 3 input channels (RGB), and weight the total summed loss by the total variation weight, $w_t$.

Now let us look at the beautiful images generated.

{{< figure src="sky1.png" lightbox="true" width="70%" height="70%" >}}
The next 3 images are the content source image at iterations 0, 100, and 199.
{{< figure src="sky2.png" lightbox="true" width="45%" height="45%" >}}
{{< figure src="sky3.png" lightbox="true" width="45%" height="45%" >}}
{{< figure src="sky4.png" lightbox="true" width="45%" height="45%" >}}

We can see what happens with the same content source image and a different style source image.

{{< figure src="art1.png" lightbox="true" width="70%" height="70%" >}}
The next 3 images are the content source image at iterations 0, 100, and 199.
{{< figure src="art2.png" lightbox="true" width="45%" height="45%" >}}
{{< figure src="featured.png" lightbox="true" width="45%" height="45%" >}}
{{< figure src="art4.png" lightbox="true" width="45%" height="45%" >}}

Lastly, perhaps the most basic style source image produces the most interesting results.

{{< figure src="drawing1.png" lightbox="true" width="60%" height="60%" >}}
The next 3 images are the content source image at iterations 0, 100, and 199.
{{< figure src="drawing2.png" lightbox="true" width="35%" height="35%" >}}
{{< figure src="drawing3.png" lightbox="true" width="35%" height="35%" >}}
{{< figure src="drawing4.png" lightbox="true" width="35%" height="35%" >}}

