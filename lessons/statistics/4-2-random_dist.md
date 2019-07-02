[Think Stats Chapter 4 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2005.html#toc41) (a random distribution)

```
# Setting up & importing necessary tools:
from __future__ import print_function, division

%matplotlib inline

import numpy as np

import nsfg
import first
import thinkstats2
import thinkplot

# Creating an array of 1000 random numbers between 0-1
numbers = np.random.random(1000)

# Creating the corresponding PMF & plotting it:
pmf = thinkstats2.Pmf(numbers)
thinkplot.Pmf(pmf)
```

The resulting PMF plot shows a relatively even distribution, with all values in the sample having an associated probability of around 0.001. This representation, however, is crowded which may obscure more subtle variations.

We now compute the CDF:

```
cdf = thinkstats2.Cdf(numbers)
thinkplot.Cdf(cdf)
```

As seen in the textbook's example of a uniform distribution, the CDF plot for the random numbers generated is also a straight line. This confirms the observation drawn from the PMF function that the distribution is indeed uniform.
