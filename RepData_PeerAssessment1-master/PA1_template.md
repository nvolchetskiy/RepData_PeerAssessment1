 "Reproducible Research" - Peer Assessment 1 -
===============================================
## Loading and preprocessing the data


```r
data <- read.csv("~/Desktop/assig1/activity.csv", colClasses = c("integer", 
    "Date", "integer"))
# head(data, n=5)
```


## What is mean total number of steps taken per day?
1. Data by day (date) and number of steps per day.
2. Histogamme.
3. Mean and mediane.


```r
n.steps <- sapply(split(data$steps, data$date), sum, na.rm = T)
hist(n.steps, main = "Histogram of the steps per day")
```

![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-2.png) 

```r
mean_ <- mean(n.steps)
median_ <- median(n.steps)
```

The mean of number of steps is **9354.2295** and mediane is **10395.**  

## What is the average daily activity pattern?
1. Split data by intervals.
2. Average of steps in each 5 minutes interval.
3. Plot 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis).
4. Find the interval that contain maximum number of steps. 


```r
avrg_interv <- sapply(split(data$steps, data$interval), mean, na.rm = T)
intervals <- unique(data$interval)
plot(x = intervals, y = avrg_interv, type = "l", xlab = "5-minute intervals", 
    ylab = "average number of step", main = "Average daily activity")
```

![plot of chunk unnamed-chunk-3](figure/unnamed-chunk-3.png) 

```r

t.interval <- sapply(split(data$steps, data$interval), sum, na.rm = T)
ind.max <- which.max(t.interval)
interval.max <- max(t.interval)
```


The 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps is **10927** and it contain **10927** steps.

## Imputing missing values
Removing all missing values form data to build a new data set.

```r
nrow(na.omit(data))
```

```
## [1] 15264
```

```r
new.data <- data
for (i in 1:nrow(data)) {
    if (is.na(data$steps[i])) {
        new.data$steps[i] <- avrg_interv[(i%%288) + 1]
    }
}
```


1. New histogamme.
2. New mean and mediane after removing missing values (NA).








