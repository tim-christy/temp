---
layout: post
title: " Central Limit Theorem"
Author: Tim Christy
---
by Tim Christy

<br>

Imagine that you want to know the mean height of everybody in Reno, NV. Since it is impractical to go out and measure the height of all 250,000+ people, you would have to rely on sample data (*randomly* sampled) to estimate this parameter. The practical application of the **central limit theorem** here says that every single possible mean we could get from our samples of size n follows a normal distribution with a mean that will be equal to the population mean so long as our sample size, n, is large enough.

<br>

To illustrate, suppose I go out and randomly survey 30 people and take the mean of their heights. Then I go out and do it again for another 30 people... and then another... and another... and so on like this until I get every possible combination of 30 people in the entire city and the mean heights of each of these combinations. The distribution of all of these mean heights form the **sampling distribution of the sample mean** for a sample size of 30. It is the distribution of every possible mean you could get from all samples of 30 people in this city.

It doesn't have to be 30 people either. There is a unique sampling distribution for every value of the sample size chosen. The distribution for samples of 15 people would look different from the sampling distribution of 30 people or 4 people or 16 people, etc. The difference would be due to the standard error; which is the standard deviation of the sampling distribution. The larger the sample size, the smaller the standard error. We will see in the example that follows.  

To illustrate that the population, does not need to be normally distributed, suppose the heights of 250,000 people follows a uniform distribution.

<br>

# Generating random height data (inches) for 250,000 people  

```Python  
import numpy as np  
import matplotlib.pyplot as plt  
%matplotlib inline  

np.random.seed(10)  
random_data = [np.random.randint(40,90) for x in range(250000)]
```

<br>

Plotting the distribution...   

<br>

```python
plt.figure(figsize=(20,10))
plt.title('A Histogram of a Very Obviously Not Normally Distributed Population', fontsize=20)
plt.xlabel('Height (in)', fontsize=15)
plt.ylabel('Frequency', fontsize=15)
plt.xticks(fontsize=15)
plt.yticks(fontsize=15)
plt.hist(random_data, bins = [40, 45, 50, 55, 60, 65, 70, 75, 80, 85, 90]);
plt.show()
```


![](../../../../assets/imgs/blogs/2020-02-01/pop_heights.png)  



This is the population distribution of every height of 250,000 people in inches. What is the mean of this population?

```python
round(np.mean(random_data),1)
```   
64.5   

<br>

Time to test the central limit theorem. It says that despite the shape of our current population distribution, the sampling distribution will be normally distributed with a mean equal to the population mean, as long as the sample size n, is large enough; typically 30 or more (there is some hand-waving going on here, but this is the gist of it). I can't take every possible mean from this population for a given value of n, but I can take enough to begin to see the sampling distributions take shape. So let's do this and check it out. We will take 10,000 samples each first of sample size 5, then 15, then 30, and then 100. We will then take the mean of each of these samples and store them in lists as shown below.  

```python  
# randomly pick 5 people from the above population, take their average, and repeat 10 times
n5 = [np.mean(np.random.choice(random_data, 5)) for x in range(10_000)]

# randomly pick 15 people from the above population, take their average, and repeat 10 times
n15 = [np.mean(np.random.choice(random_data, 15)) for x in range(10_000)]

# randomly pick 30 people, and do the same...
n30 = [np.mean(np.random.choice(random_data, 30)) for x in range(10_000)]

# randomly pick 100 people " " " " " "
n100 = [np.mean(np.random.choice(random_data, 100)) for x in range(10_000)]

```   

And now to plot these sampling distributions   

```python
plt.figure(figsize=(20,10))
plt.subplots_adjust(hspace=.5)
plots = [n5, n15, n30, n100]
labels = ['n=5', 'n=15', 'n=30', 'n=100']
counter = 0
for plot in plots:
    counter+=1
    plt.subplot(2,2,counter)
    plt.title(f'Sampling Distribution for {labels[counter-1]}', fontsize=20)
    plt.xlabel('Height (in)', fontsize=20)
    plt.ylabel('Frequency', fontsize=20)
    plt.xticks(fontsize=20)
    plt.yticks(fontsize=20)
    plt.xlim([40, 90])
    plt.hist(plot);
```   

![](../../../../assets/imgs/blogs/2020-02-01/samp_dist.png)   

# Observations

Notice that as n gets larger, the mean of the sampling distribution tightens around the population mean of 64.5. This can be explained by the standard error, which mentioned earlier, is the standard deviation of the sampling distribution. The formula is as follows  

$$SE = \frac{\sigma}{\sqrt{n}}$$

or, because you often do not have the population standard deviation, the sample standard deviation, s, is used,   

$$SE = \frac{s}{\sqrt{n}}$$  

Either way, because the standard error is inversely proportional to the sample size $n$, the larger the sample size, the smaller the standard error. This is why the sampling distributions above narrow as $n$ gets larger.  

The central limit theorem says that the sampling distribution will be normally distributed with a mean equal to the population mean; which this small simulation supports. It should be noted that there are population distributions in which this theorem will not work (see Cauchy amongst others). Also, if you know your population is normally distributed, then you can be sure that the sampling distribution will also be normally distributed.

It is also worth reiterating that the distribution of sample means is the distribution of every possible sample mean, which we did not simulate. We simulated 10,000 points per distribution, which is just an approximation to the sampling distribution of sample means. That is why the means were not equal. Despite not being exact, they did come close and improved with increasing values of n, the sample size.

This whole process works for other parameters too, not just the mean (like proportion or standard deviation).

Why does this matter? This theorem is important because it is what allows for hypothesis testing and confidence intervals. These methods rely on the assumption of a normal distribution. The central limit theorem helps to make that assumption valid.  
