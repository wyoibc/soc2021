---
title: Notebooks with RMarkdown
---


### Video recording for this session

<br>
<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/lJnATIEdV-0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>
<br><br>

This week, we revisit creating and maintaining online notebooks using RMarkdown. Two weeks ago, we worked with plain Markdown to create an example notebook. The process with RMarkdown is largely similar, but this format offers greater functionality and less typing.


<br><br>


## Table of Contents

- [1. Software Install](#software-install)

	- [1.1 Install ``RMarkdown``](#install-rmarkdown)

	- [1.2 Install ``TinyTeX``](#install-tinytex)

- [2. Data for today's exercise](#data-for-todays-exercise)

- [3. Further Reading](#further-reading)


<br><br><br><br><br>
<br><br><br><br><br>
<br><br><br><br><br>
<br><br><br><br><br>
<br><br><br><br><br>
<br><br><br><br><br>
<br><br><br><br><br>


## 1. Software Install

We will be using RStudio to create a RMarkdown document. But before we can do so, we will need to install following software:


<br>

### 1.1 Install ``RMarkdown``

- Using CRAN repository (stable version, but could be slightly stale)

```r
install.packages("rmarkdown")
```

- Development version (cutting edge) from GitHub

```r
library(devtools)

devtools::install_github("rstudio/rmarkdown")
```


<br>

### 1.2 Install ``TinyTeX``

RMarkdown is able to produce LaTeX formatted output (``.tex`` format) but it requires ``TinyTeX`` a very small and easy to maintain TeX distribution.  Installation is straightforward:

```r
install.packages("tinytex")

library(tinytex)

tinytex::install_tinytex()
```


<br><br>

## 2. Data for today's exercise

This exercise uses a population genomic data set from study of two hybridizing *Populus* species. One of the goals of this study was to uncover signatures of natural selection (*sensu* Darwin) in hybrid individuals. In order to do this, a genetic differentiation index called ``Fst`` is calculated between populations for two sets of genetic loci: those that have been determined to be under the effect of natural selection and those that are presumed neutral (i.e. no selection). We will be making a couple of figures from this data.

- ``sig.fst`` contains data for SNPs under natural selection

-  ``neu.fst`` contains data for SNPs presumed neutral 

- ``pval_counts.txt`` contains data on bootstrapping


<br><br>






## 3. Further Reading 

- [R Markdown: A Definitive Guide](https://bookdown.org/yihui/rmarkdown) by Yihui Xie, J. J. Allaire, Garrett Grolemund

- [RMarkdown Tutorial by Karl Broman](https://kbroman.org/knitr_knutshell/pages/Rmarkdown.html)

