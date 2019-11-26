---
title: Trigger Word Detection
summary: Speech recognition algorithm for trigger word detection, technology behind Alexa, Google Home, and Siri
tags:
- Speech Recognition
- Natural Language Processing
- Generative Learning
date: "2019-06-30T00:00:00Z"
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
  caption: Trigger word detection
  focal_point: Smart
  preview_only: true

url_code: "https://github.com/EricMFischer/deep-learning-specialization/blob/master/sequence-models/week-3/trigger-word-detection/Trigger%20word%20detection%20-%20v1.ipynb"
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

In the attached code I constructed a speech dataset and implemented an algorithm for trigger word detection (sometimes also called keyword detection, or wakeword detection). Trigger word detection is the technology that allows devices like Amazon Alexa, Google Home, Apple Siri, and Baidu DuerOS to wake up upon hearing a certain word.

What really is an audio recording? A microphone records little variations in air pressure over time, and it is these little variations in air pressure that your ear also perceives as sound. You can think of an audio recording is a long list of numbers measuring the little air pressure changes detected by the microphone. We will use audio sampled at $44100$ Hz (or $44100$ Hertz). This means the microphone gives us $44100$ numbers per second. Thus, a $10$ second audio clip is represented by $441000$ numbers ($10 \times 44100$).

It is quite difficult to figure out from this "raw" representation of audio whether the word "activate" was said. In order to help your sequence model more easily learn to detect triggerwords, we will compute a spectrogram of the audio. The spectrogram tells us how much different frequencies are present in an audio clip at a moment in time. Let's see an example. The graph below represents how active each frequency is (y axis) over a number of time-steps (x axis).

{{< figure src="example.png" lightbox="true" width="50%" height="50%" >}}

Once we've estimated the probability of having detected the word "activate" at each output step, we can trigger a "chiming" sound to play when the probability is above a certain threshold. This will help prevent us from inserting two chimes for a single instance of "activate". (This plays a role similar to non-max suppression from computer vision.)

With a working model for trigger word detection, I used it to make predictions on unheard audio clips (saved in wav files). In this first example, we can see that it adds a chime sound after the position where "activate" appeared in the audio sample.

{{< figure src="results.png" lightbox="true" width="50%" height="50%" >}}

Some conclusions we can draw are that data synthesis is an effective way to create a large training set for speech problems, specifically trigger word detection. Also, using a spectrogram and optionally a 1D conv layer is a common pre-processing step prior to passing audio data to an RNN, GRU or LSTM. In general, an end-to-end deep learning approach can be used to built a very effective trigger word detection system.

