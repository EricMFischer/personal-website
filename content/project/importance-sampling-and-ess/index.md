---
title: Importance Sampling and Effective Number of Samples
summary: Estimating the number of self-avoiding walks with importance sampling
tags:
- Sampling
- Markov Chain Monte Carlo
- Monte Carlo Optimization
- Importance Sampling
- Effective Sample Size
date: "2019-04-01T00:00:00Z"
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
  caption: Self-Avoiding Walk Design
  focal_point: Smart
  preview_only: true

url_code: "https://github.com/EricMFischer/importance-sampling-and-ess"
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

To estimate the total number of self-avoiding walks (SAWs) for a grid size n = 10, we will use
Monte Carlo integration. First we design a trial probability g(x) for a SAW that is easier to
sample from than the true target distribution. We then sample M SAWs from g(x) and estimate
the total count of SAWs by the mean of 1 / g(x) for SAWs x. The crux of the issue lies in how to
design g(x). Here we will examine three different designs for g(x), each assuming the grid size n
= 10 and each generating a total of M = 107 total samples.

Three Designs for g(x):

Design 1: Here g(x) is equal to the product of 1 / kj
 terms, where kj
 represents the number of
possible choices for the jth
 move. At each step j, we sample uniformly from the kj
 choices. In this
design the distribution will resemble a Gaussian because we do not constrain the length of walk.
The total estimated number K of SAWs for Design 1 was 3.1804 x 1025.

Design 2: Here g(x) is equal to the g(x) of Design 1, but multiplied by (1 - ε)m
, where ε = 0.1 is
an early termination probability at each step. This has the effect of lending shorter but more
walks overall than design 1. In the log-log plot below of K SAWs over M samples, we can see
that Design 2 obviously converges the slowest. This makes sense because Design 2 terminates
some paths early, preventing the algorithm from finding paths it might otherwise find. The total
estimated number K of SAWs for Design 2 was 3.2535 x 1025.

Design 3: This design is a modification of Design 1 to favor longer walks. For any walk longer
than 50, Design 3 generates 5 more children from that branch of the walk, reweighting
each of the children by w0
 = w / 5. This design converges the fastest. The total estimated number
K of SAWs for Design 3 was 2.0898 x 1025.

Plotting the total number of SAWs K against M = 107
 examples in the log-log plot below for
each of the Designs 1, 2, and 3, we can analyze whether the sequential importance sampling
process has converged. As expected, Design 2 has the slowest convergence after roughly M =
107
 samples due to its early termination probability. Design 3 has an improved convergence rate
over Design 1 due to the behavior of generating 5 children each time a SAW reaches a length of
50. Both Designs 1 and 3 converge after roughly M = 103
 samples, but Design 3 converges
sooner and is thus the optimal design in this study.

{{< figure src="2.png" lightbox="true" width="60%" height="60%" >}}


We can make a modification to the most optimal sampling procedure, Design 3, to investigate
the total number of self-avoiding walks that start from (0, 0) and reach a specific point (n, n).
Namely, we now only count the SAWs that successfully reach (n, n) during their walk instead of
all the SAWs. Generating 106
 samples, the true value for the total number of SAWs from (0, 0)
to (n, n) is 1.5687 x 1024.

In an effort to approximate this true value as closely as possible, I experimented with generating
3, 5, or 7 children for paths that had grown to a checkpoint length of 25, 50, 70, 80, 90, or 100
and found that it generally helps to spawn more children at a given checkpoint length, and it also
helps to increase the checkpoint length at which this happens. These conclusions are reasonable,
as the longer a SAW path is, the more “special” it is and the more unlikely it is that we have
already found SAWs that stem from this one. Of course, if the checkpoint length is too high, e.g.
200, then of course we will never even get the opportunity to generate children (because a path
will never reach that length).

Ultimately, the closest approximation to the true value of 1.5687 x 1024
 reached was for
generating 7 children once a path had reached a length of 90. For these parameters, the estimated
number of SAWs was 1.2224 x 1024.

{{< figure src="3.png" lightbox="true" width="60%" height="60%" >}}

{{< figure src="featured.png" lightbox="true" width="60%" height="60%" >}}
