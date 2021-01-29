---
title:  "Project: Scientific Data Analysis"
date:   2020-11-20
categories: [project]
tags: [Neuroscience, Analysis, Statistics]
---

Finally, some cleaning's done on [my very first Jupyter notebooks](https://github.com/soyhyoj/PGlab) created between 2018-2019. Back then, I wasn't capable of coding from scratch, so it was a process of literally copying & pasting chunks of code from the internet and running the woven code by hit-or-miss. Now that I became more proficient in Python, it was time to do some pruning and organization on these notebooks.
<br>

## Why programming?

1. Data size
    The data I used to deal with were time-series of neural signals (either electrical outputs or flourescent images) recorded over varying time length (minutes to hours) and its size would easily take up to GBs. Excel was just not enough to deal with these data and also very error-prone(due to dragging and modifying tens of thousands of rows at the same time).

2. Integrated data processing
    To analyze this kind of experimental data, multiple software (and machines) were needed at different stages of the work (collection, retrieval, analysis and visualization). A machine at imaging facility had the software for data acquisition, a machine at the lab had the licensed software for data retrieval, and then my laptop served for anlaysis and visualization. Having limited access to the licensed softwares for analysis was another issue. I wanted an integrated solution for data retrieval, processing, statistic analysis and visualization.
<br>

## Why Python?

Although I was advised to learn Matlab since it is the most abundantly used language in neuroscience laboratories, I didn't like the fact that you still need a license for its usage which I couldn't afford to. In the end, I chose Python over R only because it seemed to be the most widely used language in data sciences.
<br>

## Results (examples)

For both types of data (images and electropyshiology recordings), the raw files (.CSV) were imported as a pandas dataframe and plotted by time.

For live cell imaging data, fluorescence changes (dF = F-F0) at each timepoint relative to the first X frames of each series (F0) were calculated as (F-F0)/F0 and plotted. Each line in the below figure indicates single cell response and the red box indicates the duration of 780nm light stimulation applied to the tissue sample.
![Calcium traces from hippocampal neurons](/images/Caimage.png){:class="img-responsive"}

Local peaks(yellow dotted line) during the light stimulation from each trace were looked up from single traces. The time of appearance of the peaks were found and noted.
![Finding the timing of local peaks using idxmax](/images/Caimage-peaks.png){:class="img-responsive"}

For electrophysiology data, local peaks were detected by using find_peaks module from scipy library.
![Peak detection to count # of firing](/images/peak-detection.png){:class="img-responsive"}

After detecting the peaks, the different results from different samples were quantified for a comparison.
![Comparing # of firing](/images/quant-peaks.png){:class="img-responsive"}


## Benefits
With these codes, the time I put into the preliminary analysis was reduced from days to minutes. I could understand the results of the day in real-time and plan the next experiment based on it.
<br>

## What's next?
I'm following an [online tutorial](https://mark-kramer.github.io/Case-Studies-Python/02.html#plotting-the-erp) for advanced neural signal analysis in Python. This 