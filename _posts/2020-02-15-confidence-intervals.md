---
layout: post
title: "Confidence Intervals"
Author: Tim Christy
---
by Tim Christy  

(if you would like to view this blog in a jupyter notebook as well as all the code used, you can do so here)


# Intro  
This blog provides some intuition behind confidence intervals.

Confidence intertvals give a range of numbers in which a statistic of interest is captured a certain percentage of the time. For example, a 95% confidence interval indicates that if you calculated a confidence interval 100 times by this method, 95 or those confidence intervals would capture the statistic of interest.  

The statistic of interest is the mean. The idea is that there is some population distribution whose mean you would like to estimate. You can estimate the population mean by taking samples, so long as the sample size does not exceed 10% of the population size. If the population distribution is normal, or the sample size large enough (30 or larger; see central limit theorem) and the population is not overly skewed, the sampling distribution will also be normal. Using properties of a normal distribution, we can estimate an interval that contains the mean.  


### Assumptions
- Samples are random

- Sample sizes are done with replacement or not greater than 10% of population (samples are independent)

- Population is normally distributed or symmetric

    - If not normally distributed, then sample size greater than 30 and population not overly skewed  

The basic idea behind, random sampling methods aside, is that the sampling distribution needs to be normal for the interval to work.

Ok, proceeding now by example.  

To illustrate, we will use a very straighforward example. The population distribution will be normal. Suppose that we are trying to measure the mean height of a small country that has a population of exactly 1 million people. This is shown below where the red line is the actual population mean.


![](../../../../../assets/imgs/blogs/2020-02-15/pop_dist.png)   






This data would usually be impractical to obtain in real life (babies are born, people die, people grow, etc). It is unlikely that you will get a true snapshot of the heights of everybody in the population in time to calculate the true mean. If you had an easy way to do it though, there would be no need for confidence intervals. You could just get the acutal mean of this distribution. This is value is what we are trying to estimate by taking samples and calculating confidence intervals.

If needed, here is quick explanation of sampling distributions: From the population above a second distribution can be obtained from sample means. This is called the sampling distribution of the mean. If you go out and sample 5 people and take the mean of those 5 people, you will get one data point in the sampling distribution of the mean. If you go out and sample *every possible combination* of 5 people means the histogram will reveal the entire sampling distribution of sample means. There is a different sampling distribution for every sample size chosen. The higher the sample size, the less the distribution will vary. The mean of the sampling distribution is equal to the mean of the population distribution.

We will start with a sample size of n=5. That is, in your endeavor to get the mean height of all one million people in this country, you go out and randomly sample five people and take their mean height. The distribution below shows all the possible mean heights you could wind up with for a sample of 5 people and their associated probabilities (the higher the curve, the more probable at that height).    


![](../../../../../assets/imgs/blogs/2020-02-15/samp_dist.png)   


(Note: we only sampled 100,000 times, which is an approximation to the theoretical sampling distribution. As we run this more and more times, the simulated sampling distribution would converge to the smooth theoretical sampling distribution. For practical applications though, this is plenty to see what is happening with the population).

In real life, it is impractical to go out and take the mean of 5 people an infinite amount of times, let alone 100,000 times. It would be very difficult to obtain this distribution. But it is useful to illustrate how we estimate this mean. Because the sampling distribution is normally distributed, we can invoke the 68-95-99.7 rule, where we know that ~68% of the data lies within one standard deviation of the mean, 95% within 2 standard deviations, and 99.7% within 3 standard deviations. Since we are pretending not to have any of this data and will only get a sample to estimate, we will have to use a t-distribution. A t-distribution is essentially a normal distribution that takes a conservative estimate of the possible error. The same amount data is still contained within the same amount of standard deviations. So, let's have a look.  

First we will take one sample and see where it falls on the above distribution. So we go out and randomly select 5 people, measure their heights, take the mean of that sample, and plot it in green below.    


![](../../../../../assets/imgs/blogs/2020-02-15/one_sample.png)   


Because an arbitrary percentage of the total data possible can be captured by selecting the corresponding number of standard deviations away from the mean, we can create an interval that will capture the sample mean a certain percentage of the time. For example, if I repeat this process with a 95% confidence interval (2 standard deviations above and below the mean), this interval should catch our sample mean 95% of the time in the long run. This is demonstrated below with the two standard deviations from the mean shown in black dotted lines. They contain 95% of the possible means for this sample size.   


 ![](../../../../../assets/imgs/blogs/2020-02-15/two_sigma.png)   


 Repeating this 20 times.  


  ![](../../../../../assets/imgs/blogs/2020-02-15/twentytimes.png)   


  As shown above only one time in 20 did the sample mean fall outside of the interval between 66.42 and 73.59 inches. That is 95% of the time the sample mean falls within this interval (it didn't have to be exactly one time out of twenty, it just happened that way. The in case where you do this a very large amount of times the proportin of means that fall within this interval will converge to 95%).   

As said before, it is impractical to get this sampling distribution and to know where those boundaries are. So with confidence intervals, you simply flip the perspective. Rather than drawing the interval around the mean, we draw the interval around the mean from the sample (green line instead of red). Again, due to not knowing the sampling distribution, we do not have the standard deviation of the sampling distribution and we have to estimate it. This is done using the standard deviation of the sample, the sample size, and the t value from the corresponding t distribution (which is again, a normal distribution that errs conservatively because of the extra uncertainty added from using the standard error from a single sample). The formula is as follows.  

$$\bar{x} \pm t * \frac{s}{\sqrt{n}}$$   

where $\bar{x}$ is the mean of the individual sample, t is the t value, s is the standard deviation of the individual sample, and n is the sample size. The way we find the t-value here depends on the level of confidence we would like. To find the value we use ``scipy.stats.t.ppf()``. This function returns a t-value if you provide the percentage under the distribution desired and the degrees of freedom. Since the distribution is symmetric and the total area sums to 1, for a 95% interval, we want the t-value that occurs at either 2.5% or 97.5%. The t-value that occurs at 2.5% will be the negative of the t-value that occurs at 97.5%. Because of this, a total of 5% will be excluded from the interval (2.5% on each side of the distribution).  

The degree of freedom is just the sample size minus one (dof = n-1).   

Your t-value is what determines your level of confidence. You must decide what level suits the application. For this blog, we will use 95% as shown below.   

![](../../../../../assets/imgs/blogs/2020-02-15/confidence_int.png)    

Notice how this time, the green line moves around with the confidence interval (black dotted lines). Keep in mind that in typical applications, we do not see the blue distribution and its mean shown in red. We only see the green line and the black dotted lines (the sample mean and the 95% confidence interval respectively). This does illustrate though that the interval is often captures the mean for a 95% confidence level.

Occasionally the interval does miss. A higher confidence level can be chosen, but it will expand the range that the confidence interval spans. The best way to improve your confidence interval is to increase your sample size, though there is a diminishing returns effect on this improvement as the sample size increases.  

Up to now we have been working with a sample size of n=5. Everything works well because our population is normally distributed, but in reality, it is very unlikely we will ever know anything about the shape of the population distribution. A large enough sample size is important because even if the population distribution is not normal we can be confident that the sampling distribution will be normally distributed via the central limit theorem (unless the population distribution is very skewed). A larger sample size also shrinks the width of the confidence interval because the sampling distribution tightens up. This is due to the standard error, which is the standard deviation of the sampling distribution and defined as follows

$$SE = \frac{s}{\sqrt{n}}$$

where s is the standard deviation of the sample, and n is the sampling size. As n increases the standard error decreases. This is shown graphically below for three sampling distributions where n=5, n=30, and n=100.   


![](../../../../../assets/imgs/blogs/2020-02-15/samp_dists.png)     


Confidence intervals for 5 random samples of each of these sample sizes are shown below. The distribution has been removed and each individual sample mean is shown as a blue dot with the confidence intervals spanning from it. The true population mean is shown as a red line down the middle. When a given interval contains the red line, it catches the true mean. Notice the improvement in the estimation as the sample size increases.   


![](../../../../../assets/imgs/blogs/2020-02-15/conf_ints.png)    


# Final Thoughts

Above we went over how to calculate confidence intervals for the mean. There are other parameters in which you can use this same method, though some of the formulas and assumptions change. It is important to be sure that your sampling distribution is normal, otherwise the above method may give you inaccurate results. For large sample sizes a normal sampling distribution assumption is usually valid, with large meaning 30 or greater. If a small sample size is unavoidable and you cannot assume a normal population distribution, there are other methods to get around this issue like parameterization or bootstrapping (future blogs).

Also note that statisticians are particular about the language used to describe the confidence interval. You should not say anything that gives the impression that the mean is variable while the interval is constant like, "95% of the time the mean will be found in this interval". This statement is not correct. It is that 95% of the time, this method will capture the mean. The interval is what is variable, not the mean.   

The end. Thanks for reading.
