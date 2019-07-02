[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

First we construct the actual distribution of the number of children under the age of 18 in each household:

```
# Importing all the necessary packages
from __future__ import print_function, division

%matplotlib inline

import numpy as np

import nsfg
import first
import thinkstats2
import thinkplot

# Loading in the corresponding data
resp = nsfg.ReadFemResp()

# Using in-built Pmf method to created PMF:
actual_distrib = thinkstats2.Pmf(resp['numkdhh'], label='actual')
```
The resulting PMF returns: {0: 0.466178202276593, 1: 0.21405207379301322, 2: 0.19625801386889966, 3: 0.08713855815779145, 4: 0.025644380478869556, 5: 0.01072877142483318}

Then we build the corresponding biased distribution based on the same data:

```
# Create a function to build biased distribution by multiplying each value by its probability
def BiasPmf(pmf, label):
    new_pmf = pmf.Copy(label=label)
    for x, p in pmf.Items():
        new_pmf.Mult(x, x)
    new_pmf.Normalize()
    return new_pmf

biased_distrib = BiasPmf(pmf, 'observed')
```
The resulting biased distribution looks like this: {0: 0.0, 1: 0.20899335717935616, 2: 0.38323965252938175, 3: 0.25523760858456823, 4: 0.10015329586101177, 5: 0.052376085845682166}

Now we plot both overlayed:

```
thinkplot.PrePlot(2)
thinkplot.Pmfs([actual_distrib, biased_distrib])
thinkplot.Show(xlabel='children under 18', ylabel='PMF')

# Calculate mean of unbiased and biased distributions:
actual_distrib.Mean(), biased_distrib.Mean()
```
The resulting step function for the unbiased distribution suggests there are more families with 0 children under the age of 18 (and that the distribution is positively skewed) whereas that of the biased distribution is more normally distributed with its measures of central tendency indicating a majority of ~2 children under the age of 18 per household. Indeed, the means for each distribution are ~1.024 and ~2.404 respectively.

