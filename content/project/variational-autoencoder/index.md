---
title: Formulation of Variational Lower Bound and Application of VAE to MNIST Dataset
summary: Formulation of the evidence lower bound (ELBO) for the variational autoencoder and an application to synthesizing binary images
tags:
- Variational Autoencoder
- Autoencoder
- Inference Network
- Generative Modeling
- Computer Vision
date: "2019-06-04T00:00:00Z"
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
  caption:
  focal_point: Smart
  preview_only: true

# links:
# - icon: github
#   icon_pack: fab
#   name: Follow
#   url: https://github.com/ericmfischer
url_code: "https://github.com/EricMFischer/variational-autoencoder"
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

An autoencoder is a type of artificial neural network that learns efficient data codings, i.e. performs feature detection, in an unsupervised manner. It learns an encoding, or representation, for a set of data usually for the purposes of dimensionality reduction. In addition to the this reduction, the autoencoder has a reconstruction side, in which it generates from a reduced encoding a representation as similar as possible to the original to the original input.

The VAE uses a Bayesian neural network, which extends a standard artificial neural network with posterior inference. A Bayesian neural network, by placing a prior distribution on its weights, is able to capture a measure of uncertainty in predictions that a neural network cannot. From a probabilistic perspective, this is crucial. The MLE that neural networks perform to determine weight values ignores any uncertainty in e.g. the weight values or the even the choice of MLE as an optimization method.

Also, neural networks are well-known to be susceptible to overfitting due to no quantification of uncertainty, and thus they employ techniques such as L2 regularization (which from a Bayesian perspective is equivalent to inducing prior distributions on the weights). Neural network optimization in this case is akin to searching for maximum _a posteriori_ estimators rather than MLE. Although this works well in practice, from a probabilistic perspective it only alleviates the overfitting issue but does not solve it. Hence, we have a motivation for Bayesian neural networks: to lend a probabilistic interpretation of the neural network with which we can perform posterior inference.

We can observe some generated images by the VAE. For much more, see the attached Full Paper.

{{< figure src="2.png" lightbox="true" width="40%" height="40%" >}}

I would like to extend this project to work with an infinite mixture of Gaussian distributions, in addition to the mixture of binomial distributions used for the MNIST data in the attached Full Paper. This would allow us to reperform similar experiments with the CIFAR-10 dataset, applying the variational autoencoder to natural images with diverse structure.
