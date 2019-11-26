---
title: Facial Trait and Political Election Analysis by SVM
summary: Trained SVM classifiers to infer 14 facial traits from low-level image features and use that information to make election predictions
tags:
- SVM
- Pattern Recognition
- Computer Vision
- Histogram of Oriented Gradients
date: "2018-11-24T00:00:00Z"
# featured: false

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
url_code: "https://github.com/EricMFischer/svm-political-election"
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

Here we follow the paper by Jungseock et al. in ICCV 2015. The rationale is that election outcomes can be predicted solely based on geometric and appearance facial features. Further, these features can be mapped to high-level concepts of perception such as attractiveness or trustworthiness.

We exploit such low-level facial features and high-level concepts of perception to analyze election outcomes and party affiliations (GOP vs DEM) of politicians. The goal is to train classifiers that can infer the perceived face social traits from low-level features and apply the model to analyze the outcomes of real-world political elections.

**Classification by Landmarks**<br />
I used the Scikit-learn library to train 14 Support Vector Regression models, one for each attribute dimension (e.g. old, masculine, etc.) of the training examples. I performed k-fold cross-validation with $5$ folds and an 80/20 train/test split and used GridSearchCV from Scikit-learn to optimize the SVR parameters. The optimal C, γ, and ε (C, gamma, epsilon) values were searched for in the following ranges:

$C ∈ [2^5, 2^3, …, 2^{15}]$<br />
$γ ∈ [2^15, 2^13, …, 2^3]$<br />
$ε ∈ [2^7, 2^5, 2^3, 2^1]$

The optimal $C$, $γ$, and $ε$ (C, gamma, epsilon) values found with the Radial Basis Function (RBF) kernel are summarized below.

{{< figure src="hyperparameters.png" lightbox="true" width="60%" height="60%" >}}

**Classification by Rich Features** <br />
By concatenating for each of the 491 images the original landmark features and HoG (histogram of oriented gradient) features extracted from an image, and then retraining the 14 SVR trait models with these new features, we can observe improved training and testing accuracy and precision in almost all the models individually.

After training, I applied the 14 learned classifiers to the test examples left out of training, and I measured performance (i.e. classification average accuracy and precision) of the classifiers. As I used a regression analysis for the trait models, to perform classification, the real-valued scores of the predicted test labels and the ground-truth test labels were converted to a [-1, 1] binary classification based on a threshold specific to each trait: the mean of the ground-truth label for that trait across the 491 images supplied as data.

This shows the average accuracy for training and testing data for each of the 14 SVR trait models.

{{< figure src="14_trait_accuracies.png" lightbox="true" width="60%" height="60%" >}}

This shows the average accuracy for training and testing data for each of the 14 SVR rich trait models (trained with landmarks and HoG features), in comparison with the 14 SVR trait models trained with only landmark features.

{{< figure src="14_trait_rich_poor_accuracies.png" lightbox="true" width="60%" height="60%" >}}

All models have improved training accuracy and precision, and all but two models have improved testing accuracy and precision, when using HoG features in addition to landmarks. This demonstrates that HoG features improve the binary classification performance.
