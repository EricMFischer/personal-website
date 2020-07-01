---
title: Deep Generative Classifier with Short Run Inference
summary: Deep generative classifier employs Short Run Markov Chain Monte Carlo inference with Langevin dynamics and backpropagation through time
tags:
- Markov Chain Monte Carlo
- Computer Vision
- Generative Modeling
- Unsupervised Learning
- Backpropagation through Time
- Langevin Dynamics
- Short Run Inference
- Adversarial Robustness
date: "2020-06-12T00:00:00Z"
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
  caption: Center for Vision, Cognition, Learning, and Autonomy at UCLA
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
I completed my Masters thesis while advised by Dr. Song-Chun Zhu at the Center for Vision, Cognition, Learning, and Autonomy at UCLA.

A deep generative classifier employs Short Run Markov Chain Monte Carlo inference with Langevin dynamics and backpropagation through time. In contrast to a convolutional neural network (ConvNet) with analogous architecture, the Short Run classifier approaches the same classification accuracy and (1) may synthesize data, (2) may learn unsupervised from additional unannotated data, and (3) exhibits robustness to adversarial attacks, due to the stochasticity of the Langevin equation and the top-down architecture of the generator network. The ConvNet classifier lacks the ability to perform (1) or (2) and possesses no defense against adversarial attacks, a critical concern for any deployed machine learning system. Meanwhile, the Short Run classifier demonstrates the capacity to improve in both classification accuracy and the quality of data synthesis, given additional unannotated data.

{{< figure src="1.png" lightbox="true" width="90%" height="90%" >}}
{{< figure src="2.png" lightbox="true" width="90%" height="90%" >}}
{{< figure src="3.png" lightbox="true" width="90%" height="90%" >}}
{{< figure src="4.png" lightbox="true" width="90%" height="90%" >}}
{{< figure src="5.png" lightbox="true" width="90%" height="90%" >}}
{{< figure src="6.png" lightbox="true" width="90%" height="90%" >}}
{{< figure src="7.png" lightbox="true" width="85%" height="85%" >}}
{{< figure src="8.png" lightbox="true" width="85%" height="85%" >}}
{{< figure src="9.png" lightbox="true" width="85%" height="85%" >}}
{{< figure src="10.png" lightbox="true" width="85%" height="85%" >}}
{{< figure src="11.png" lightbox="true" width="85%" height="85%" >}}
