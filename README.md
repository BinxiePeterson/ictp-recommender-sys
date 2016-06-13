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

```javascript
## [1] "Jester5k"   "MSWeb"      "MovieLense"
```
data(MovieLense)
class(MovieLense)
## [1] "realRatingMatrix"
## attr(,"package")
## [1] "recommenderlab"
