---
title:  "Project: Research Trend Analysis"
date:   2020-09-17
categories: [project]
tags: [Neuroscience, NLP, Trend, Analysis, CodeOp]
---

As a neuroscience geek who has recently moved on to the field of data science, it was very clear to me that the first personal analytics project had to be something related to my dear past experience of being a neuroscientist.

[The Journal of Neuroscience](https://www.jneurosci.org/), a weekly peer-reviewed journal published by [the Society for Neuroscience](https://www.sfn.org/), is probably the journal which I (like any other scientists working in this domain) have read the most while designing, developing and concluding experiments.

This 2-week sprint project was a perfect opportunity for me to leverage common NLP techniques in order to find an answer to my question:
Were the rising topics that I read as trends result of my attentional bias or was there a real fuss about them?

![term-frequency](/images/project-research-trend.png){:class="img-responsive"}

From the beginning, this project was meant to be a cleaning-oriented one and I definitely enjoyed the wrangling part a lot.
But the best part of this work is that I actually got to visualize some of the most stunning trends I've been observing these years: the efforts in academia to defeat the sexual bias prevalent in animal experiments (scroll back and check the keywords including 'male' or 'female' from the graph above. What you see in the graph is the changes in the relative term frequency of indicated keywords during the last 10 years.)

[Female mammals have long been neglected in biomedical research](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3008499/) and not until recently did the investigators selectively choose male animals for behavioral experiments for the 'consistency' of their results. In 2012, I was actually advised not to include female animals to the behavior studies since 'female behaviors are unstable and it can cause trouble when trying to publish the work'.

:zany_face:

Now the situation has changed. All the researchers have obligation to justify their choice when the study was based on a single-sex group (at least in the European research centers where I worked). And this inclusion kicked in quite radically around the year of 2016, as the result of this analysis suggests. Probably it is because [the National Institutes of Health (NIH) grants started to ask for all applicants to design experiments accounting for Sex as a Biological Variable (SABV) as of Jan 2016](https://grants.nih.gov/grants/guide/notice-files/not-od-15-102.html).

OK, so the most frequently appeared terms over the last 3-4 years have been 'female' & 'male' with a reason. What else did I find from this data? Well, rather traditional subjects such as perception (keywords: 'hair cell', 'visual cortex'), decision making (keyword: 'prefrontal cortex'), memory (keywords: 'synaptic plasticity', 'working memory') and brain activity monitoring (keyword: 'firing rate', 'action potential', 'magnetic resonance', 'neural activity') were captured and they are actually steady-selling topics over decades with some ebbs and flows.

This project still has some room for improvement. Some articles of particular releases were not collected due to API problems. Also, the final ngrams can be more specified by filtering out generic terms without relevant information about articles' topics like 'mechanism underlying', 'present study', 'significance statement'. Lastly, I would like to investigate the possibility to aggregate the popular research terms by topics using modeling in NLP.

For more details on how I processed this data: [check my notebooks](https://github.com/soyhyoj/ResearchTrendAnalysis)
