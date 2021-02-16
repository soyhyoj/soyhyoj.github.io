---
title:  "Setting up R environment with Anaconda"
date:   2021-2-X
categories: [Programming]
tags: [R]
---



[tutorial for creating an environment with R](https://docs.anaconda.com/anaconda/user-guide/tasks/using-r-language/)
# Create a new conda environment with all the r-essentials
`conda create -n r_env r-essentials r-base`

# Activate the environment
`conda activate r_env`

# Update R packages
`conda update r-caret`

# Install RStudio
`conda install -c r rstudio`

# Run RStudio
`rstudio`



# Install R packages using conda
Add r- before the packagename:
`conda install r-packagename`

[Installing R package within a R-env with conda]("../images/")


Using the rstudio within the R environment solved issues regarding package install -> why?


for some packages like inspectdf:
```
conda install conda-build
conda skeleton cran <something_on_cran>
conda build r-<something_on_cran_lowercased>
conda install -c local r-<something_on_cran_lowercased>
```
