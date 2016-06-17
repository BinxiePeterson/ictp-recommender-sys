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
e) Examine the image and ensure you understand what it illustrates.

## Lab 2. Recommendation Models.
a) Display the model applicable to the objects of type *realRatingMatrix* using *recommenderRegistry$get_entries*:

```
recommender_models <- recommenderRegistry$get_entries(dataType = "realRatingMatrix")
names(recommender_models)
```
How many models are listed?

b) Describe these models

```
lapply(recommender_models, "[[", "description")
```

c) We plan to use IBCF and UBCF. Check the parameters of these two models.

```
recommender_models$IBCF_realRatingMatrix$parameters
```

```
recommender_models$UBCF_realRatingMatrix$parameters
```

d) List the parameters of these two model. What do they mean?

## Lab 3. Data Exploration

a) Initial exploration of data types and dimensions

```
dim(MovieLense)
```

```
## [1]  943 1664
```
```
slotNames(MovieLense)
```
```
## [1] "data"      "normalize"
```
```
class(MovieLense@data)
```
```
## [1] "dgCMatrix"
## attr(,"package")
## [1] "Matrix"
```

```
dim(MovieLense@data)
```

```
## [1]  943 1664
```

b) Exploring values of ratings

```
vector_ratings <- as.vector(MovieLense@data)
unique(vector_ratings) # what are unique values of ratings
```

```
## [1] 5 4 0 3 1 2
```

```
table_ratings <- table(vector_ratings) # what is the count of each rating value
table_ratings
```

```
## vector_ratings
##       0       1       2       3       4       5 
## 1469760    6059   11307   27002   33947   21077
```


c) Visualize the rating:

```
vector_ratings <- vector_ratings[vector_ratings != 0] # rating == 0 are NA values
vector_ratings <- factor(vector_ratings)

qplot(vector_ratings) + 
  ggtitle("Distribution of the ratings")
```

d) Examine the image and ensure you understand what it illustrates.

e) Exploring viewings of movies:

```
views_per_movie <- colCounts(MovieLense) # count views for each movie

table_views <- data.frame(movie = names(views_per_movie),
                          views = views_per_movie) # create dataframe of views
table_views <- table_views[order(table_views$views, 
                                 decreasing = TRUE), ] # sort by number of views

ggplot(table_views[1:6, ], aes(x = movie, y = views)) +
  geom_bar(stat="identity") + 
  theme(axis.text.x = element_text(angle = 45, hjust = 1)) + 
ggtitle("Number of views of the top movies")
```
f) What are the top movies listed?

g) Exploring average ratings:

```
average_ratings <- colMeans(MovieLense)

qplot(average_ratings) + 
  stat_bin(binwidth = 0.1) +
  ggtitle("Distribution of the average movie rating")
```


  
