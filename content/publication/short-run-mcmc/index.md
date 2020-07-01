---
title: Learning Multi-Layer Latent Variable Model with Short Run MCMC Inference Dynamics
summary: Short Run MCMC sampling is utilized in a deep generative model with multiple layers of latent variables
tags:
- Computer Vision
- Markov Chain Monte Carlo
- CNN
- Langevin Dynamics
- Energy Based Model
- Short-Run MCMC
- Generative Modeling
- GAN
- Variational Autoencoder
- Residual Network
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
url_pdf: "https://arxiv.org/abs/1912.01909"
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
# slides: example
---
I ran experiments for this paper, submitted to CVPR, while advised by Dr. Song-Chun Zhu at the Center for Vision, Cognition, Learning, and Autonomy at UCLA.

The short-run Markov Chain Monte Carlo model can be considered a valid generative model just like
a variational autoencoder (VAE) or a generative adversarial network (GAN). We use it to synthesize, interpolate, and reconstruct
images. Image synthesis is performed by running Langevin dynamics from a uniform noise distribution, and the interpolation
and reconstruction results rival or are qualitatively better than a VAE and GAN.

A presentation I gave about a related paper is below.

<iframe src="https://docs.google.com/presentation/d/e/2PACX-1vTwqWIG_fIb6ZLkgt-gvPCFICmBBC5C4qUC9qRLHeVKR9qdaye4w-sbobeTfbQFK6r2Vrdg5m9W2-q8/embed?start=true&loop=false&delayms=5000" frameborder="0" width="675" height="405" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>

{{< figure src="1.png" lightbox="true" width="90%" height="90%" >}}
{{< figure src="2.png" lightbox="true" width="90%" height="90%" >}}
{{< figure src="3.png" lightbox="true" width="90%" height="90%" >}}
{{< figure src="4.png" lightbox="true" width="90%" height="90%" >}}
{{< figure src="5.png" lightbox="true" width="90%" height="90%" >}}
{{< figure src="6.png" lightbox="true" width="90%" height="90%" >}}
{{< figure src="7.png" lightbox="true" width="85%" height="85%" >}}
{{< figure src="8.png" lightbox="true" width="85%" height="85%" >}}
