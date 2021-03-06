
<!-- README.md is generated from README.Rmd. Please edit that file -->
<img src="img/R_badge.png" width="40%" style="display: block; margin: auto 0 auto auto;" />

KMediansR
=========

[![Build Status](https://travis-ci.org/UBC-MDS/KMediansR.svg?branch=master)](https://travis-ci.org/UBC-MDS/KMediansR)

The goal of KMediansR is to group a set of objects in such a way that objects in the same group (called a cluster) are more similar (in some sense or another) to each other than to those in other groups (clusters). In k-medians clustering, we partition `n` observations into `k` clusters. It calculates the median for each cluster to determine its centroid. The `kmedians` package performs k-medians clustering on the dataset entered by the users and returns clustered data. This can prove to be an extremely beneficial package as k-medians is more robust to outliers than the arithmetic mean(k-means).

Functions included
==================

The three main functions in the package are :

1.  `distance` function

    -   The function helps to calculate the Manhattan distance between each pair of the two collection inputs. This function takes as input

    1.  An `mxn` array of `m` original observations in an `n`-dimensional space
    2.  An `pxk` array of `p` original observations in an `k`-dimensional space It returns a `mxp` distance matrix. For each `i` and `j`, the mteric `distance(u=X[i], v=Y[j])` is computed and stored in the `ij`th entry

2.  `kmedian` function

    -   A quick implementation of k-medians. It takes as input

    1.  A 2D array of data
    2.  The desired number of clusters It returns
    3.  A 2D array of the medians
    4.  1D array of labels (the clusters the points belongs to)

3.  `summary` function

    -   This function generates the descriptive statistics that summarize the implementation of the `kmedians` function on the input data. It returns a dataframe that contains information about the model run such as the number of clusters, the number of points in each cluster, the inter and intra cluster distance

Usage
=====

Simple example demonstrating the functionality of this package:

``` r
# load package
library(KMediansR)

# toy data with two clusters                    
toy_data <- matrix(
  c(1,1,1,2,2,1,100,100,101,100,100,101),
  nrow = 6,
  ncol = 2,
  byrow = TRUE)

# initialize the cluster centers                                 
m <- matrix(
  c(1,1,100,100),
  nrow = 2,
  ncol = 2,
  byrow = TRUE)

# calculate Manhanttan distance between the medians and data points
manhanttan_distance <- distance(X = toy_data, medians = m)

     [,1] [,2]
[1,]    0  198
[2,]    1  197
[3,]    1  197
[4,]  198    0
[5,]  199    1
[6,]  199    1

# cluster the data points                                        
clustered <- kmedians(X = toy_data, num_clusters = 2)

[[1]]
     [,1] [,2]
[1,]    1    1
[2,]  100  100

[[2]]
[1] 1 1 1 2 2 2

# generate summary results                                       
report <- summary(X = toy_data, medians = clustered[[1]], labels = clustered[[2]])

  Cluster.Label Median.Coordinates Number.of.Points.in.Cluster Average.Distance  Minimum.Distance Maximum.Distance
1             1                1,1                           3        0.6666667                 0                1
2             2            100,100                           3        0.6666667                 0                1
```

Existing packages in the R environment
======================================

`kGmedian` : This is a fast k-medians clustering based on recursive averaged stochastic gradient algorithms. The advantage of the `kGmedian` algorithm compared to `kmeans` strategy is that it deals with sum of norms instead of sum of squared norms, ensuring a more robust behaviour against outlying values.

Subject to change
=================

The above ideas are presented as a part of the initial proposal. However, they could be subject to change in the following milestones based on the project timeline or technical complexity.

Dependencies
============

-   R Version 3.5.2

-   R libraries:
    -   `dplyr` Version 0.7.8
    -   `magrittr` Version 1.5

Installation
============

You can install the released version of KMediansR from [CRAN](https://CRAN.R-project.org) with:

``` r
library(dplyr)
library(magrittr)
devtools::install_github("UBC-MDS/KMediansR")
```
