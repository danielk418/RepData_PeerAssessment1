---
title: "Reproducible Research: Peer Assessment 1"
output: 
  html_document:
    keep_md: true
---



## Loading and preprocessing the data

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
#1 Unzip data

unzip(zipfile = "activity.zip", exdir = "data")

#2 Load the data 
activity_data <- read.csv("data/activity.csv")

#3 Process/transform the data (if necessary) into a format suitable for your analysis. Ignore(Remove?) missing values

activity_data_no_nulls <- activity_data[complete.cases(activity_data), ]
```


## What is mean total number of steps taken per day?


```r
library(kableExtra)
```

```
## 
## Attaching package: 'kableExtra'
```

```
## The following object is masked from 'package:dplyr':
## 
##     group_rows
```

```r
#1 What is mean total number of steps taken per day?
total_steps_data <- activity_data_no_nulls %>% 
                    group_by(date) %>% 
                    summarize(total_steps = sum(steps))
```



```r
total_sample <- head(total_steps_data, 10)

kable(x = total_steps_data, caption = "Mean Total Number of Steps Taken Per Day", col.names = c("Date", "Total Steps"))%>%
  kable_styling(bootstrap_options = c("striped", "hover"),full_width = FALSE)
```

<table class="table table-striped table-hover" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption>Mean Total Number of Steps Taken Per Day</caption>
 <thead>
  <tr>
   <th style="text-align:left;"> Date </th>
   <th style="text-align:right;"> Total Steps </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> 2012-10-02 </td>
   <td style="text-align:right;"> 126 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-03 </td>
   <td style="text-align:right;"> 11352 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-04 </td>
   <td style="text-align:right;"> 12116 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-05 </td>
   <td style="text-align:right;"> 13294 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-06 </td>
   <td style="text-align:right;"> 15420 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-07 </td>
   <td style="text-align:right;"> 11015 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-09 </td>
   <td style="text-align:right;"> 12811 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-10 </td>
   <td style="text-align:right;"> 9900 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-11 </td>
   <td style="text-align:right;"> 10304 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-12 </td>
   <td style="text-align:right;"> 17382 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-13 </td>
   <td style="text-align:right;"> 12426 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-14 </td>
   <td style="text-align:right;"> 15098 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-15 </td>
   <td style="text-align:right;"> 10139 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-16 </td>
   <td style="text-align:right;"> 15084 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-17 </td>
   <td style="text-align:right;"> 13452 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-18 </td>
   <td style="text-align:right;"> 10056 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-19 </td>
   <td style="text-align:right;"> 11829 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-20 </td>
   <td style="text-align:right;"> 10395 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-21 </td>
   <td style="text-align:right;"> 8821 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-22 </td>
   <td style="text-align:right;"> 13460 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-23 </td>
   <td style="text-align:right;"> 8918 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-24 </td>
   <td style="text-align:right;"> 8355 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-25 </td>
   <td style="text-align:right;"> 2492 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-26 </td>
   <td style="text-align:right;"> 6778 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-27 </td>
   <td style="text-align:right;"> 10119 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-28 </td>
   <td style="text-align:right;"> 11458 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-29 </td>
   <td style="text-align:right;"> 5018 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-30 </td>
   <td style="text-align:right;"> 9819 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-10-31 </td>
   <td style="text-align:right;"> 15414 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-02 </td>
   <td style="text-align:right;"> 10600 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-03 </td>
   <td style="text-align:right;"> 10571 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-05 </td>
   <td style="text-align:right;"> 10439 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-06 </td>
   <td style="text-align:right;"> 8334 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-07 </td>
   <td style="text-align:right;"> 12883 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-08 </td>
   <td style="text-align:right;"> 3219 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-11 </td>
   <td style="text-align:right;"> 12608 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-12 </td>
   <td style="text-align:right;"> 10765 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-13 </td>
   <td style="text-align:right;"> 7336 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-15 </td>
   <td style="text-align:right;"> 41 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-16 </td>
   <td style="text-align:right;"> 5441 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-17 </td>
   <td style="text-align:right;"> 14339 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-18 </td>
   <td style="text-align:right;"> 15110 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-19 </td>
   <td style="text-align:right;"> 8841 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-20 </td>
   <td style="text-align:right;"> 4472 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-21 </td>
   <td style="text-align:right;"> 12787 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-22 </td>
   <td style="text-align:right;"> 20427 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-23 </td>
   <td style="text-align:right;"> 21194 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-24 </td>
   <td style="text-align:right;"> 14478 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-25 </td>
   <td style="text-align:right;"> 11834 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-26 </td>
   <td style="text-align:right;"> 11162 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-27 </td>
   <td style="text-align:right;"> 13646 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-28 </td>
   <td style="text-align:right;"> 10183 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 2012-11-29 </td>
   <td style="text-align:right;"> 7047 </td>
  </tr>
</tbody>
</table>



```r
#2 Make a histogram of the total number of steps taken each day
hist(total_steps_data$total_steps, xlab = "Daily Steps", main = "Histogram of total number of steps taken each day")
```

![](PA1_template_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

```r
dev.copy(png, file = "plots/hist_total_steps_per_day.png")
```

```
## png 
##   3
```

```r
dev.off()
```

```
## png 
##   2
```

```r
#3 Calculate and report the mean and median of the total number of steps taken per day

step_mean <-  round(mean(total_steps_data$total_steps)) 

step_median <- round(median(total_steps_data$total_steps))

mean_and_median <- as.data.frame(cbind(step_mean, step_median))

kable(x = mean_and_median, caption = "Mean and Median of the Total Number of Steps Taken Per Day", col.names = c("Mean", "Median"))%>%
  kable_styling(bootstrap_options = c("striped", "hover"),full_width = FALSE)
```

<table class="table table-striped table-hover" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption>Mean and Median of the Total Number of Steps Taken Per Day</caption>
 <thead>
  <tr>
   <th style="text-align:right;"> Mean </th>
   <th style="text-align:right;"> Median </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 10766 </td>
   <td style="text-align:right;"> 10765 </td>
  </tr>
</tbody>
</table>


## What is the average daily activity pattern?


```
## [1] 1
```

<table class="table table-striped table-hover" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption>Average Daily Activity Pattern</caption>
 <thead>
  <tr>
   <th style="text-align:right;"> Interval </th>
   <th style="text-align:right;"> Avg Steps Per Interval </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 0 </td>
   <td style="text-align:right;"> 1.7169811 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 5 </td>
   <td style="text-align:right;"> 0.3396226 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 10 </td>
   <td style="text-align:right;"> 0.1320755 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 15 </td>
   <td style="text-align:right;"> 0.1509434 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 20 </td>
   <td style="text-align:right;"> 0.0754717 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 25 </td>
   <td style="text-align:right;"> 2.0943396 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 30 </td>
   <td style="text-align:right;"> 0.5283019 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 35 </td>
   <td style="text-align:right;"> 0.8679245 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 40 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 45 </td>
   <td style="text-align:right;"> 1.4716981 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 50 </td>
   <td style="text-align:right;"> 0.3018868 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 55 </td>
   <td style="text-align:right;"> 0.1320755 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 100 </td>
   <td style="text-align:right;"> 0.3207547 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 105 </td>
   <td style="text-align:right;"> 0.6792453 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 110 </td>
   <td style="text-align:right;"> 0.1509434 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 115 </td>
   <td style="text-align:right;"> 0.3396226 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 120 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 125 </td>
   <td style="text-align:right;"> 1.1132075 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 130 </td>
   <td style="text-align:right;"> 1.8301887 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 135 </td>
   <td style="text-align:right;"> 0.1698113 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 140 </td>
   <td style="text-align:right;"> 0.1698113 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 145 </td>
   <td style="text-align:right;"> 0.3773585 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 150 </td>
   <td style="text-align:right;"> 0.2641509 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 155 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 200 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 205 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 210 </td>
   <td style="text-align:right;"> 1.1320755 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 215 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 220 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 225 </td>
   <td style="text-align:right;"> 0.1320755 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 230 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 235 </td>
   <td style="text-align:right;"> 0.2264151 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 240 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 245 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 250 </td>
   <td style="text-align:right;"> 1.5471698 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 255 </td>
   <td style="text-align:right;"> 0.9433962 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 300 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 305 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 310 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 315 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 320 </td>
   <td style="text-align:right;"> 0.2075472 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 325 </td>
   <td style="text-align:right;"> 0.6226415 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 330 </td>
   <td style="text-align:right;"> 1.6226415 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 335 </td>
   <td style="text-align:right;"> 0.5849057 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 340 </td>
   <td style="text-align:right;"> 0.4905660 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 345 </td>
   <td style="text-align:right;"> 0.0754717 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 350 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 355 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 400 </td>
   <td style="text-align:right;"> 1.1886792 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 405 </td>
   <td style="text-align:right;"> 0.9433962 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 410 </td>
   <td style="text-align:right;"> 2.5660377 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 415 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 420 </td>
   <td style="text-align:right;"> 0.3396226 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 425 </td>
   <td style="text-align:right;"> 0.3584906 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 430 </td>
   <td style="text-align:right;"> 4.1132075 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 435 </td>
   <td style="text-align:right;"> 0.6603774 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 440 </td>
   <td style="text-align:right;"> 3.4905660 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 445 </td>
   <td style="text-align:right;"> 0.8301887 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 450 </td>
   <td style="text-align:right;"> 3.1132075 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 455 </td>
   <td style="text-align:right;"> 1.1132075 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 500 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 505 </td>
   <td style="text-align:right;"> 1.5660377 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 510 </td>
   <td style="text-align:right;"> 3.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 515 </td>
   <td style="text-align:right;"> 2.2452830 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 520 </td>
   <td style="text-align:right;"> 3.3207547 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 525 </td>
   <td style="text-align:right;"> 2.9622642 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 530 </td>
   <td style="text-align:right;"> 2.0943396 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 535 </td>
   <td style="text-align:right;"> 6.0566038 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 540 </td>
   <td style="text-align:right;"> 16.0188679 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 545 </td>
   <td style="text-align:right;"> 18.3396226 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 550 </td>
   <td style="text-align:right;"> 39.4528302 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 555 </td>
   <td style="text-align:right;"> 44.4905660 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 600 </td>
   <td style="text-align:right;"> 31.4905660 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 605 </td>
   <td style="text-align:right;"> 49.2641509 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 610 </td>
   <td style="text-align:right;"> 53.7735849 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 615 </td>
   <td style="text-align:right;"> 63.4528302 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 620 </td>
   <td style="text-align:right;"> 49.9622642 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 625 </td>
   <td style="text-align:right;"> 47.0754717 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 630 </td>
   <td style="text-align:right;"> 52.1509434 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 635 </td>
   <td style="text-align:right;"> 39.3396226 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 640 </td>
   <td style="text-align:right;"> 44.0188679 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 645 </td>
   <td style="text-align:right;"> 44.1698113 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 650 </td>
   <td style="text-align:right;"> 37.3584906 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 655 </td>
   <td style="text-align:right;"> 49.0377358 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 700 </td>
   <td style="text-align:right;"> 43.8113208 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 705 </td>
   <td style="text-align:right;"> 44.3773585 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 710 </td>
   <td style="text-align:right;"> 50.5094340 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 715 </td>
   <td style="text-align:right;"> 54.5094340 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 720 </td>
   <td style="text-align:right;"> 49.9245283 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 725 </td>
   <td style="text-align:right;"> 50.9811321 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 730 </td>
   <td style="text-align:right;"> 55.6792453 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 735 </td>
   <td style="text-align:right;"> 44.3207547 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 740 </td>
   <td style="text-align:right;"> 52.2641509 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 745 </td>
   <td style="text-align:right;"> 69.5471698 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 750 </td>
   <td style="text-align:right;"> 57.8490566 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 755 </td>
   <td style="text-align:right;"> 56.1509434 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 800 </td>
   <td style="text-align:right;"> 73.3773585 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 805 </td>
   <td style="text-align:right;"> 68.2075472 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 810 </td>
   <td style="text-align:right;"> 129.4339623 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 815 </td>
   <td style="text-align:right;"> 157.5283019 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 820 </td>
   <td style="text-align:right;"> 171.1509434 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 825 </td>
   <td style="text-align:right;"> 155.3962264 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 830 </td>
   <td style="text-align:right;"> 177.3018868 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 835 </td>
   <td style="text-align:right;"> 206.1698113 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 840 </td>
   <td style="text-align:right;"> 195.9245283 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 845 </td>
   <td style="text-align:right;"> 179.5660377 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 850 </td>
   <td style="text-align:right;"> 183.3962264 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 855 </td>
   <td style="text-align:right;"> 167.0188679 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 900 </td>
   <td style="text-align:right;"> 143.4528302 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 905 </td>
   <td style="text-align:right;"> 124.0377358 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 910 </td>
   <td style="text-align:right;"> 109.1132075 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 915 </td>
   <td style="text-align:right;"> 108.1132075 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 920 </td>
   <td style="text-align:right;"> 103.7169811 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 925 </td>
   <td style="text-align:right;"> 95.9622642 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 930 </td>
   <td style="text-align:right;"> 66.2075472 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 935 </td>
   <td style="text-align:right;"> 45.2264151 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 940 </td>
   <td style="text-align:right;"> 24.7924528 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 945 </td>
   <td style="text-align:right;"> 38.7547170 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 950 </td>
   <td style="text-align:right;"> 34.9811321 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 955 </td>
   <td style="text-align:right;"> 21.0566038 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1000 </td>
   <td style="text-align:right;"> 40.5660377 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1005 </td>
   <td style="text-align:right;"> 26.9811321 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1010 </td>
   <td style="text-align:right;"> 42.4150943 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1015 </td>
   <td style="text-align:right;"> 52.6603774 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1020 </td>
   <td style="text-align:right;"> 38.9245283 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1025 </td>
   <td style="text-align:right;"> 50.7924528 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1030 </td>
   <td style="text-align:right;"> 44.2830189 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1035 </td>
   <td style="text-align:right;"> 37.4150943 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1040 </td>
   <td style="text-align:right;"> 34.6981132 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1045 </td>
   <td style="text-align:right;"> 28.3396226 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1050 </td>
   <td style="text-align:right;"> 25.0943396 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1055 </td>
   <td style="text-align:right;"> 31.9433962 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1100 </td>
   <td style="text-align:right;"> 31.3584906 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1105 </td>
   <td style="text-align:right;"> 29.6792453 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1110 </td>
   <td style="text-align:right;"> 21.3207547 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1115 </td>
   <td style="text-align:right;"> 25.5471698 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1120 </td>
   <td style="text-align:right;"> 28.3773585 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1125 </td>
   <td style="text-align:right;"> 26.4716981 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1130 </td>
   <td style="text-align:right;"> 33.4339623 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1135 </td>
   <td style="text-align:right;"> 49.9811321 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1140 </td>
   <td style="text-align:right;"> 42.0377358 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1145 </td>
   <td style="text-align:right;"> 44.6037736 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1150 </td>
   <td style="text-align:right;"> 46.0377358 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1155 </td>
   <td style="text-align:right;"> 59.1886792 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1200 </td>
   <td style="text-align:right;"> 63.8679245 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1205 </td>
   <td style="text-align:right;"> 87.6981132 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1210 </td>
   <td style="text-align:right;"> 94.8490566 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1215 </td>
   <td style="text-align:right;"> 92.7735849 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1220 </td>
   <td style="text-align:right;"> 63.3962264 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1225 </td>
   <td style="text-align:right;"> 50.1698113 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1230 </td>
   <td style="text-align:right;"> 54.4716981 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1235 </td>
   <td style="text-align:right;"> 32.4150943 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1240 </td>
   <td style="text-align:right;"> 26.5283019 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1245 </td>
   <td style="text-align:right;"> 37.7358491 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1250 </td>
   <td style="text-align:right;"> 45.0566038 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1255 </td>
   <td style="text-align:right;"> 67.2830189 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1300 </td>
   <td style="text-align:right;"> 42.3396226 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1305 </td>
   <td style="text-align:right;"> 39.8867925 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1310 </td>
   <td style="text-align:right;"> 43.2641509 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1315 </td>
   <td style="text-align:right;"> 40.9811321 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1320 </td>
   <td style="text-align:right;"> 46.2452830 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1325 </td>
   <td style="text-align:right;"> 56.4339623 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1330 </td>
   <td style="text-align:right;"> 42.7547170 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1335 </td>
   <td style="text-align:right;"> 25.1320755 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1340 </td>
   <td style="text-align:right;"> 39.9622642 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1345 </td>
   <td style="text-align:right;"> 53.5471698 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1350 </td>
   <td style="text-align:right;"> 47.3207547 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1355 </td>
   <td style="text-align:right;"> 60.8113208 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1400 </td>
   <td style="text-align:right;"> 55.7547170 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1405 </td>
   <td style="text-align:right;"> 51.9622642 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1410 </td>
   <td style="text-align:right;"> 43.5849057 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1415 </td>
   <td style="text-align:right;"> 48.6981132 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1420 </td>
   <td style="text-align:right;"> 35.4716981 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1425 </td>
   <td style="text-align:right;"> 37.5471698 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1430 </td>
   <td style="text-align:right;"> 41.8490566 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1435 </td>
   <td style="text-align:right;"> 27.5094340 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1440 </td>
   <td style="text-align:right;"> 17.1132075 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1445 </td>
   <td style="text-align:right;"> 26.0754717 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1450 </td>
   <td style="text-align:right;"> 43.6226415 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1455 </td>
   <td style="text-align:right;"> 43.7735849 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1500 </td>
   <td style="text-align:right;"> 30.0188679 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1505 </td>
   <td style="text-align:right;"> 36.0754717 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1510 </td>
   <td style="text-align:right;"> 35.4905660 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1515 </td>
   <td style="text-align:right;"> 38.8490566 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1520 </td>
   <td style="text-align:right;"> 45.9622642 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1525 </td>
   <td style="text-align:right;"> 47.7547170 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1530 </td>
   <td style="text-align:right;"> 48.1320755 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1535 </td>
   <td style="text-align:right;"> 65.3207547 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1540 </td>
   <td style="text-align:right;"> 82.9056604 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1545 </td>
   <td style="text-align:right;"> 98.6603774 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1550 </td>
   <td style="text-align:right;"> 102.1132075 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1555 </td>
   <td style="text-align:right;"> 83.9622642 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1600 </td>
   <td style="text-align:right;"> 62.1320755 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1605 </td>
   <td style="text-align:right;"> 64.1320755 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1610 </td>
   <td style="text-align:right;"> 74.5471698 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1615 </td>
   <td style="text-align:right;"> 63.1698113 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1620 </td>
   <td style="text-align:right;"> 56.9056604 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1625 </td>
   <td style="text-align:right;"> 59.7735849 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1630 </td>
   <td style="text-align:right;"> 43.8679245 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1635 </td>
   <td style="text-align:right;"> 38.5660377 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1640 </td>
   <td style="text-align:right;"> 44.6603774 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1645 </td>
   <td style="text-align:right;"> 45.4528302 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1650 </td>
   <td style="text-align:right;"> 46.2075472 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1655 </td>
   <td style="text-align:right;"> 43.6792453 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1700 </td>
   <td style="text-align:right;"> 46.6226415 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1705 </td>
   <td style="text-align:right;"> 56.3018868 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1710 </td>
   <td style="text-align:right;"> 50.7169811 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1715 </td>
   <td style="text-align:right;"> 61.2264151 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1720 </td>
   <td style="text-align:right;"> 72.7169811 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1725 </td>
   <td style="text-align:right;"> 78.9433962 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1730 </td>
   <td style="text-align:right;"> 68.9433962 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1735 </td>
   <td style="text-align:right;"> 59.6603774 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1740 </td>
   <td style="text-align:right;"> 75.0943396 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1745 </td>
   <td style="text-align:right;"> 56.5094340 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1750 </td>
   <td style="text-align:right;"> 34.7735849 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1755 </td>
   <td style="text-align:right;"> 37.4528302 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1800 </td>
   <td style="text-align:right;"> 40.6792453 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1805 </td>
   <td style="text-align:right;"> 58.0188679 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1810 </td>
   <td style="text-align:right;"> 74.6981132 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1815 </td>
   <td style="text-align:right;"> 85.3207547 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1820 </td>
   <td style="text-align:right;"> 59.2641509 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1825 </td>
   <td style="text-align:right;"> 67.7735849 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1830 </td>
   <td style="text-align:right;"> 77.6981132 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1835 </td>
   <td style="text-align:right;"> 74.2452830 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1840 </td>
   <td style="text-align:right;"> 85.3396226 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1845 </td>
   <td style="text-align:right;"> 99.4528302 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1850 </td>
   <td style="text-align:right;"> 86.5849057 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1855 </td>
   <td style="text-align:right;"> 85.6037736 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1900 </td>
   <td style="text-align:right;"> 84.8679245 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1905 </td>
   <td style="text-align:right;"> 77.8301887 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1910 </td>
   <td style="text-align:right;"> 58.0377358 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1915 </td>
   <td style="text-align:right;"> 53.3584906 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1920 </td>
   <td style="text-align:right;"> 36.3207547 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1925 </td>
   <td style="text-align:right;"> 20.7169811 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1930 </td>
   <td style="text-align:right;"> 27.3962264 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1935 </td>
   <td style="text-align:right;"> 40.0188679 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1940 </td>
   <td style="text-align:right;"> 30.2075472 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1945 </td>
   <td style="text-align:right;"> 25.5471698 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1950 </td>
   <td style="text-align:right;"> 45.6603774 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 1955 </td>
   <td style="text-align:right;"> 33.5283019 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2000 </td>
   <td style="text-align:right;"> 19.6226415 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2005 </td>
   <td style="text-align:right;"> 19.0188679 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2010 </td>
   <td style="text-align:right;"> 19.3396226 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2015 </td>
   <td style="text-align:right;"> 33.3396226 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2020 </td>
   <td style="text-align:right;"> 26.8113208 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2025 </td>
   <td style="text-align:right;"> 21.1698113 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2030 </td>
   <td style="text-align:right;"> 27.3018868 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2035 </td>
   <td style="text-align:right;"> 21.3396226 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2040 </td>
   <td style="text-align:right;"> 19.5471698 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2045 </td>
   <td style="text-align:right;"> 21.3207547 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2050 </td>
   <td style="text-align:right;"> 32.3018868 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2055 </td>
   <td style="text-align:right;"> 20.1509434 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2100 </td>
   <td style="text-align:right;"> 15.9433962 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2105 </td>
   <td style="text-align:right;"> 17.2264151 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2110 </td>
   <td style="text-align:right;"> 23.4528302 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2115 </td>
   <td style="text-align:right;"> 19.2452830 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2120 </td>
   <td style="text-align:right;"> 12.4528302 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2125 </td>
   <td style="text-align:right;"> 8.0188679 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2130 </td>
   <td style="text-align:right;"> 14.6603774 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2135 </td>
   <td style="text-align:right;"> 16.3018868 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2140 </td>
   <td style="text-align:right;"> 8.6792453 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2145 </td>
   <td style="text-align:right;"> 7.7924528 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2150 </td>
   <td style="text-align:right;"> 8.1320755 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2155 </td>
   <td style="text-align:right;"> 2.6226415 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2200 </td>
   <td style="text-align:right;"> 1.4528302 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2205 </td>
   <td style="text-align:right;"> 3.6792453 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2210 </td>
   <td style="text-align:right;"> 4.8113208 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2215 </td>
   <td style="text-align:right;"> 8.5094340 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2220 </td>
   <td style="text-align:right;"> 7.0754717 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2225 </td>
   <td style="text-align:right;"> 8.6981132 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2230 </td>
   <td style="text-align:right;"> 9.7547170 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2235 </td>
   <td style="text-align:right;"> 2.2075472 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2240 </td>
   <td style="text-align:right;"> 0.3207547 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2245 </td>
   <td style="text-align:right;"> 0.1132075 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2250 </td>
   <td style="text-align:right;"> 1.6037736 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2255 </td>
   <td style="text-align:right;"> 4.6037736 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2300 </td>
   <td style="text-align:right;"> 3.3018868 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2305 </td>
   <td style="text-align:right;"> 2.8490566 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2310 </td>
   <td style="text-align:right;"> 0.0000000 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2315 </td>
   <td style="text-align:right;"> 0.8301887 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2320 </td>
   <td style="text-align:right;"> 0.9622642 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2325 </td>
   <td style="text-align:right;"> 1.5849057 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2330 </td>
   <td style="text-align:right;"> 2.6037736 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2335 </td>
   <td style="text-align:right;"> 4.6981132 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2340 </td>
   <td style="text-align:right;"> 3.3018868 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2345 </td>
   <td style="text-align:right;"> 0.6415094 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2350 </td>
   <td style="text-align:right;"> 0.2264151 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2355 </td>
   <td style="text-align:right;"> 1.0754717 </td>
  </tr>
</tbody>
</table>

![](PA1_template_files/figure-html/total steps-1.png)<!-- -->

```
## png 
##   3
```

```
## png 
##   2
```

```
## [1] "The 5 minute interval with the maximum number of steps is 835 ."
```



## Imputing missing values



```r
#1 Calculate and report the total number of missing values in the dataset (i.e. the total number of rows with NAs)

nrow(activity_data[!complete.cases(activity_data), ]) 
```

```
## [1] 2304
```

```r
#2 Devise a strategy for filling in all of the missing values in the dataset. The strategy does not need to be sophisticated. For example, you could use the mean/median for that day, or the mean for that 5-minute interval, etc.

mean_steps_per_interval <- activity_data %>% 
                           group_by(interval) %>% 
                           summarize(avg = mean(steps, na.rm = TRUE))

null_records <- activity_data[!complete.cases(activity_data), ]

#merge null records with mean steps per interval
merged_data <- merge(x = mean_steps_per_interval, y = null_records, by.x = "interval", by.y = "interval")

filled_in_records <-  merged_data %>% 
                      select(-steps) %>% 
                      rename(steps = avg)

#3 Create a new dataset that is equal to the original dataset but with the missing data filled in.

imputed_data <-  rbind(filled_in_records, activity_data[complete.cases(activity_data), ])

imputed_data_grouped <- imputed_data %>% 
                        group_by(date) %>% 
                        summarize(total_steps_imputed = sum(steps))


#4 Make a histogram of the total number of steps taken each day and Calculate and report the mean and median total number of steps taken per day. Do these values differ from the estimates from the first part of the assignment? What is the impact of imputing missing data on the estimates of the total daily number of steps?

hist(imputed_data_grouped$total_steps_imputed, xlab = "Daily Steps", main = "Histogram of total number of steps taken each day (imputed data)")
```

![](PA1_template_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

```r
dev.copy(png, file="plots/hist_daily_steps_taken_imputed.png")
```

```
## png 
##   3
```

```r
dev.off()
```

```
## png 
##   2
```

```r
summary(imputed_data_grouped$total_steps_imputed)[4:3]
```

```
##     Mean   Median 
## 10766.19 10766.19
```

```r
imputed_mean <- toString(round(summary(imputed_data_grouped$total_steps_imputed)[[4]],2)) 

imputed_median <- toString(round(summary(imputed_data_grouped$total_steps_imputed)[[3]],2)) 

non_imputed_mean <- toString(round(summary(total_steps_data$total_steps)[[4]], 2)) 

non_imputed_median <- toString(round(summary(total_steps_data$total_steps)[[3]], 2))  
```



## Are there differences in activity patterns between weekdays and weekends?


```r
#1 Create a new factor variable in the dataset with two levels – “weekday” and “weekend” indicating whether a given date is a weekday or weekend day.

imputed_data$date_type <- as.factor(ifelse(test = weekdays(as.Date(imputed_data$date)) %in% c("Saturday", "Sunday"), yes = "weekend", no = "weekday"))     

#2 Make a panel plot containing a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all weekday days or weekend days (y-axis).

weekday_data <- imputed_data[imputed_data$date_type == "weekday", ]

weekday_data_grouped <- weekday_data %>% 
                        group_by(interval) %>% 
                        summarize(avg_steps = mean(steps))
             
weekend_data <- imputed_data[imputed_data$date_type == "weekend", ]

weekend_data_grouped <- weekend_data %>% 
                        group_by(interval) %>% 
                        summarize(avg_steps = mean(steps))



par(mfrow=c(2,1))

with(weekend_data_grouped, plot(type="l", x = interval, y = avg_steps, ylab= "Number of Steps"))
title(main = "weekend")

with(weekday_data_grouped, plot(type="l", x = interval, y = avg_steps, ylab= "Number of Steps"))
title(main = "weekday")
```

![](PA1_template_files/figure-html/unnamed-chunk-5-1.png)<!-- -->

```r
dev.copy(png, file = "plots/panel_plot_number_of_steps.png")
```

```
## png 
##   3
```

```r
dev.off()
```

```
## png 
##   2
```

```r
print("The panel plots show that there are significant differences between the Weeknd and Weekday activity patterns.")
```

```
## [1] "The panel plots show that there are significant differences between the Weeknd and Weekday activity patterns."
```
