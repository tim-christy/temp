---
layout: page
title: Quick Reference for Descriptive Statistics
author: Tim Christy
---



 1. [Measures of Central Tendency](#measures-of-cental-tendency)
    1. [Mean](#mean)  
    1. [Median](#median)  
    1. [Mode](#mode)  



<br>

### Measures of Central Tendency
In any given data set, the values of those data tend to have some point in which they cluster around. Some measures of the value they cluster around are described by the mean, median, and mode.  

<br>
#### Mean
The mean is the sum of all the individual values divided by the number of values there are. Given a set of data: $$[x_1, x_2, x_3, ..., x_n]$$, the mean of the data is defined as follows

$$\bar{x} = \frac{\sum_{i=1}^n x_i}{n}$$  

It is worth noting that the mean is sensitive to outliers. For example, if you have a dataset consisting of [1, 2, 3, 4, 5, 6000] the mean of this dataset will be mainly influenced by the last datapoint in that set. The mean for this set is 1002.5 even though most of the values a very small.

<br>

#### Median
The median is the middle value, or 50th percentile, in a data set. That is if you were to arrange all the values from smallest to largest, the median value would be the middle datapoint (or if there are two middle datapoints, the mean of the two middle points). Here are two examples:  

1) $$A = [5, 7, 8, 1, 4, 9, 3]$$  

For dataset A, we first arrange all values in numerical order like so  

$$A = [1, 3, 4, 5, 7, 8, 9]$$  

We see that the middle value is 5 because there are 3 datapoints to the left and 3 data points to the right of the number 5 in the list. This is the median of this dataset.  

2) $$B = [6, 3, 7, 2, 4, 10]$$  

For dataset B, we proceed as before  

$$B = [2, 3, 4, 6, 7, 10]$$  

and see that there are two middle points- 4 and 6. We take the mean of the two and that is the median for this data set (which is 5)

$$\frac{4+6}{2} = 5$$   

As opposed to the mean, the median is unaffected by outliers which can make it a viable alternative in some situations where outliers exist.


<br>
#### Mode
The mode is simply the most popular value in the dataset (or the most frequently occurring value). The way I remember it is that in French "à la mode", as in "Pie à la Mode", means "in the current fashion" which I further translate to what is "popular". The mode is what's most popular in a dataset.
