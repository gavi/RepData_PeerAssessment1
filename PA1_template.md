# Reproducible Research: Peer Assessment 1


## Loading and preprocessing the data

```r
library(data.table)
data<-fread("activity.csv")
#Convert date column to date field
data$date<-as.Date(data$date,format="%Y-%m-%d")
```



## What is mean total number of steps taken per day?

```r
library(plyr)
total_steps<-ddply(data,"date",summarise,total.steps=sum(steps,na.rm=T))
hist(total_steps$total.steps)
```

![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-2.png) 
# Mean

```r
mean(total_steps$total.steps)
```

```
## [1] 9354
```
# Median

```r
median(total_steps$total.steps)
```

```
## [1] 10395
```
## What is the average daily activity pattern?

# 5 minute interval plot


```r
#We need ggplot for this
library(ggplot2)
#Lets summarize the data
interval_steps<-ddply(data,"interval",summarise,avg.steps=mean(steps,na.rm=T))
head(interval_steps)
```

```
##   interval avg.steps
## 1        0   1.71698
## 2        5   0.33962
## 3       10   0.13208
## 4       15   0.15094
## 5       20   0.07547
## 6       25   2.09434
```

```r
ggplot(data=interval_steps,aes(x=interval,y=avg.steps))+geom_line()
```

![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-5.png) 


## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
