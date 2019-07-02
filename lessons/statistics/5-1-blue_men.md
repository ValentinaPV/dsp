[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

```
# Setting up everything necessary:
from __future__ import print_function, division

%matplotlib inline

import nsfg
import first
import analytic

import thinkstats2

import scipy.stats
```

Given the assumption that the distribution of heights in BRFSS is approximately normal, we will build a model normal distribution of male heights with the paramteres provided: μ = 178 and σ = 7.7

```
# Creating model distribution
distribution = scipy.stats.norm.cdf(loc=178, scale=7.7)
```

Now that we have the distribution, we can answer the question of what percentage of th US population falls between the 5'10" and 6'1" requirement by calculating the CDF of each. Note: 5'10" is 177.8cm and 6'1" is 185.42cm

```
short = dist.cdf(177.8)
tall = dist.cdf(185.42)
short, tall
```

This reveals that approximately 49% of the US's male population is 5'10" or shorter and 83% are 6'1" or shorter. Therefore the percentage of US males within that range can be found by subtracting the two values:

```
acceptable_range = tall - short
acceptable_range
```

Therefore approximately 34% of US males are between the 5'10" and 6'1" mark, thereby making them eligible to join the Blue Man Group.
