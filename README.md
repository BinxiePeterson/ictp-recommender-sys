# ICTP-Recommender-Sys
# Building a Recommender System in R

In this Hands-On Exercise, you will build a simple recommender system in R using the techniques you have just learned. There are 7 sections. Please ensure you complete each section before you move the the next one.

## Used Packages

```sh
#install.packages("recommenderlab")
library(recommenderlab)
library(ggplot2)
```

## Load Data

```sh
set.seed(1)
data_package <- data(package = "recommenderlab")
data_package$results[, "Item"]
```````
 
```
## [1] "Jester5k"   "MSWeb"      "MovieLense"
```

```sh
data(MovieLense)
class(MovieLense)
```

```
## [1] "realRatingMatrix"
## attr(,"package")
## [1] "recommenderlab"
```

## Lab 1. Computing the Similarity Matrix

a) Determine how similar the first four USERS are with each other

```
similarity_users <- similarity(MovieLense[1:4, ], 
                               method = "cosine", 
                               which = "users")
```                               

b) Convert similarity_users class into a matrix and visualize it

```
as.matrix(similarity_users)
```
```
##            1          2          3          4
## 1 0.00000000 0.16893670 0.03827203 0.06634975
## 2 0.16893670 0.00000000 0.09706862 0.15310468
## 3 0.03827203 0.09706862 0.00000000 0.33343036
## 4 0.06634975 0.15310468 0.33343036 0.00000000
```
```
image(as.matrix(similarity_users), main = "User similarity")
```

c) Examine the image and ensure you understand what it illustrates.

d) Compute and visualize the similarity between the first four ITEMS

```
similarity_items <- similarity(MovieLense[, 1:4], method =
                                 "cosine", which = "items")
```
```
as.matrix(similarity_items)
```
```
##                   Toy Story (1995) GoldenEye (1995) Four Rooms (1995) Get Shorty (1995)
## Toy Story (1995)         0.0000000        0.4023822         0.3302448        0.4549379
## GoldenEye (1995)         0.4023822        0.0000000         0.2730692        0.5025708
## Four Rooms (1995)        0.3302448        0.2730692         0.0000000        0.3248664
## Get Shorty (1995)        0.4549379        0.5025708         0.3248664        0.0000000
```

```
image(as.matrix(similarity_items), main = "Item similarity")
```
**e) Examine the image and ensure you understand what it illustrates.**
