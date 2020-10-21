---
title:  "Garbage in, garbage out: Dealing with outliers"
date:   2020-10-21
categories: [Interview]
tags: [Time-series, Data preprocessing, Statistics, Data Analytics]
---

Recently I was asked to justify my choice of leaving outliers -instead of removing them- during a technical interview for a data scientist position. The interview was based on a pre-handed take-home test where I provided a time series forecast related to a specific business case.

Among the numerous questions I got from two interviewers over an hour, the one about outliers raised me a particular interest. Despite the confidence in my rationale built on a substantial EDA, their response was cluing me that they were clearly not happy with the way I dealt with the outliers. According to the on-site feedback, I had to exclude those values from the data before fitting a predictive algorithm.

To determine whether to retain, eliminate, or replace detected outliers, one should take into account not only the source/type of the data but also the cause/purpose of the preprocessing. This time I obviously made a naive mistake by betraying the basic principle of computer science: [Garbage in, garbage out](https://en.wikipedia.org/wiki/Garbage_in,_garbage_out). In my defense, there was some transition shock.

The confusion mainly came from the fact that the outliers presented in this particular assignment were **correctly measured** out-of-range values. To add more context, I have been trained to collect and analyze experimental data in biology labs for years. In basic science research, what's important is what you **observe**, not what you expect from the data. [Since an extreme value itself is a natural event however rare its probability, it would be unethical to intentionally exclude a part of the data from the rest unless there is an obvious doubt in its acquisition (e.g. failed to control conditions, fundamental errors in measurements).](https://bolt.mph.ufl.edu/6050-6052/unit-1/one-quantitative-variable-introduction/understanding-outliers/)

There is no more dreadful and disgusting thing than 'data manipulation(=fabrication)' in life science research, and selectively choosing which sample to include for statistical testing belongs to it. Thus I was naturally prone to be conservative of some of the data preprocessing techniques (imputing missing values, removing null records, and excluding outliers) in modeling and that was clearly a bad practice in machine learning. [Handling outliers can depend on 'domain knowledge'](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#sec21). It's what I've overlooked in this recent task by naively applying the rule I was familiar with ('Do not exclude!') to the data in hand.

A transition takes effort, time, courage, and flexibility - understanding differences and embracing new rules. I didn't get the job but lessons were priceless.
