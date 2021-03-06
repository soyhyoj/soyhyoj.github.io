---
title:  "Project: Research Trend Analysis"
date:   2020-09-17
categories: [project]
tags: [Neuroscience, NLP, Trend, Analysis, CodeOp]
---

As a neuroscience geek who has recently moved on to the field of data science, it was very clear to me that the first personal analytics project had to be something related to my dear past experience of being a neuroscientist.

[The Journal of Neuroscience](https://www.jneurosci.org/), a weekly peer-reviewed journal published by [the Society for Neuroscience](https://www.sfn.org/), is probably one of the journals that I have read the most while designing, developing and conducting experiments.

This 2-week sprint project was a perfect opportunity for me to leverage common NLP techniques in order to find an answer to my question:
Were the rising topics that I read as trends result of my attentional bias or was there a real fuss about them?

![term-frequency](/images/project-research-trend.png){:class="img-responsive"}

From the beginning, this project was meant to be a cleaning-oriented one and I definitely enjoyed the wrangling part a lot. But the best part of this work is that I actually got to visualize some of the most stunning trends I've been observing these years: the efforts in academia to defeat the sexual bias prevalent in animal experiments<br> (Scroll back and check the keywords including 'male' or 'female' from the graph above. What you see in the graph is the changes in the relative term frequency of indicated keywords during the last 10 years.)

[Female mammals have long been neglected in biomedical research](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3008499/) and not until recently did the investigators consider female samples for behavioral experiments in order to ensure the 'consistency' of their results. In 2012, I was actually advised not to include female animals for behavior studies since 'female behaviors are unstable and it can only cause trouble when trying to publish the work'.

Now the situation has changed. All the researchers have obligation to justify their choice when the study was based on a single-sex group (at least in the European research centers where I belonged). And this inclusion kicked in quite radically around the year 2016, as the result of this analysis suggests. Probably we cannot neglect the fact that this time window coincides with when [the National Institutes of Health (NIH) grants started to ask for all applicants to design experiments accounting for Sex as a Biological Variable (SABV)](https://grants.nih.gov/grants/guide/notice-files/not-od-15-102.html). Now the scientists are strongly encouraged to involve both sexes in their study and the effort has been visible at least from my point of view.

OK, so the most frequently appeared terms over the last 3-4 years have been **'female' & 'male'** with a reason. What else did I find from this data?

Rather traditional subjects such as **perception** (keywords: 'hair cell', 'visual cortex'), **decision making** (keyword: 'prefrontal cortex'), **memory** (keywords: 'synaptic plasticity', 'working memory') and **brain activity monitoring** (keyword: 'firing rate', 'action potential', 'magnetic resonance', 'neural activity') were captured and they are actually steady-selling topics for over decades with some ebbs and flows.

This project has some room for improvement. Some articles of particular releases were not collected due to API problems. Also, the final selection of terms can be refined by filtering out generic terms like 'mechanism underlying', 'present study', or 'significance statement' (these are not giving any information about the subjects). Lastly, I would like to investigate the possibility to aggregate the popular research terms by topics using modeling in NLP.

For more details on how I processed this data: [check my notebooks](https://github.com/soyhyoj/ResearchTrendAnalysis)
