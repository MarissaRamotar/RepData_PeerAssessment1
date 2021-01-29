---
title: "Reproducible Research: Peer Assessment 1"
output: 
  html_document:
    keep_md: true
---


## Loading and preprocessing the data

### Load Packages


```r
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
library(ggplot2)
```

### Load data


```r
# Reading in CSV data using readr package and read_csv function

path <- file.path("activity", "activity.csv")

activity <- readr::read_csv(file = path)
```

```
## Parsed with column specification:
## cols(
##   steps = col_double(),
##   date = col_date(format = ""),
##   interval = col_double()
## )
```

<p>&nbsp;</p>
#### Examining file 


```r
str(activity)
```

```
## tibble [17,568 x 3] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ steps   : num [1:17568] NA NA NA NA NA NA NA NA NA NA ...
##  $ date    : Date[1:17568], format: "2012-10-01" "2012-10-01" ...
##  $ interval: num [1:17568] 0 5 10 15 20 25 30 35 40 45 ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   steps = col_double(),
##   ..   date = col_date(format = ""),
##   ..   interval = col_double()
##   .. )
```

<p>&nbsp;</p>
#### Creating new file grouped by days across the two months and removing NA for this part of assignment.


```r
Totalactivity <- activity %>% 
group_by(date) %>% 
  filter(!is.na(steps)) %>% 
  summarise(totalsteps=sum(steps))
```

```
## `summarise()` ungrouping output (override with `.groups` argument)
```

## What is mean total number of steps taken per day?

* Histogram showing total number of steps taken each day


```r
Totalactivity %>% 
ggplot(mapping = aes(x = totalsteps)) +
  geom_histogram(fill = "blue")+
  labs(x ="Total numbers of steps in a day", y="Count")+
  ggtitle("History showing total number of steps taken each day")
```

```
## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
```

![](PA1_template_files/figure-html/unnamed-chunk-5-1.png)<!-- -->


## What is the average daily activity pattern?



## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
