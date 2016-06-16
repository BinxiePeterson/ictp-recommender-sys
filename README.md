# ICTP-Recommender-Sys
# Building a Recommender System in R

In this Hands-On Exercise, you will build a simple recommender system in R using the techniques you have just learned. There are 7 sections. Please ensure you complete each section before you move the the next one.

# Used Packages

```sh
#install.packages("recommenderlab")
library(recommenderlab)
library(ggplot2)
```

# Load Data

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

### Lab 1. Computing the Similarity Matrix

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
