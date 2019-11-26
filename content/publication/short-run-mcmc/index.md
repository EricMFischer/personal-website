---
title: Short-Run MCMC Residual Network toward Energy Based Model
summary: Non-convergent non-persistent short-run MCMC residual network beats VAE and GAN for image synthesis, interpolation, and reconstruction
tags:
- Computer Vision
- Markov Chain Monte Carlo
- CNN
- Langevin Dynamics
- Energy Based Model
- Short-Run MCMC
- Generative Learning
- GAN
- Variational Autoencoder
date: "2019-10-15T00:00:00Z"
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
  caption: Short-Run MCMC interpolation between synthesized examples
  focal_point: Smart
  preview_only: false

url_code: ""
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

The short-run Markov Chain Monte Carlo model from this paper (Arxiv link soon) is a valid generative model just like
a variational autoencoder (VAE) or a generative adversarial network (GAN). We use it to synthesize, interpolate, and reconstruct
images. Image synthesis is performed by running Langevin dynamics from a uniform noise distribution. And the interpolation
and reconstruction results rival or are better than VAE and GAN.

Please note that although this paper has been submitted to CVPR and is under review, the final draft is still being finalized. As a result, all the images and content here are taken from a predecessor paper (arxiv.org/abs/1904.09770) to which I personally did not contribute.

As soon as the paper for this study is finished, I will write about it and include its illustrations here, along with removing the present content. In the meantime,  some illustrations and the abstract for a predessor paper "On Learning Non-Convergent Non-Persistent Short-Run MCMC Toward Energy-Based Model" are included for reference:

**Abstract**: This paper studies a curious phenomenon in learning energy-based model (EBM)
using MCMC. In each learning iteration, we generate synthesized examples by
running a non-convergent, non-mixing, and non-persistent short-run MCMC toward
the current model, always starting from the same initial distribution such as uniform
noise distribution, and always running a fixed number of MCMC steps. After
generating synthesized examples, we then update the model parameters according
to the maximum likelihood learning gradient, as if the synthesized examples are fair
samples from the current model. We treat this non-convergent short-run MCMC
as a learned generator model or a flow model. We provide arguments for treating
the learned non-convergent short-run MCMC as a valid model. We show that
the learned short-run MCMC is capable of generating realistic images. More
interestingly, unlike traditional EBM or MCMC, the learned short-run MCMC is
capable of reconstructing observed images and interpolating between images,
like generator or flow models.

{{< figure src="1.png" lightbox="true" width="90%" height="90%">}}
{{< figure src="2.png" lightbox="true" width="90%" height="90%">}}
{{< figure src="3.png" lightbox="true" width="85%" height="85%" >}}
{{< figure src="4.png" lightbox="true" width="90%" height="90%" >}}
{{< figure src="5.png" lightbox="true" width="90%" height="90%" >}}
{{< figure src="6.png" lightbox="true" width="90%" height="90%">}}
{{< figure src="7.png" lightbox="true" width="85%" height="85%" >}}
{{< figure src="8.png" lightbox="true" width="85%" height="85%" >}}

