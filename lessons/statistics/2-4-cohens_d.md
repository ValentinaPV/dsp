[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

```
# Import all the important things for the exercise

from __future__ import print_function, division
%matplotlib inline

import numpy as np
import nsfg
import first
import thinkstats2

# Import pregnancy data
preg = nsfg.ReadFemPreg()

# Separate data into first-borns vs all others, assuming we're only interested in live births

live = preg[preg.outcome == 1]
firsts = live[live.birthord == 1]
others = live[live.birthord != 1]

first_weight = firsts.totalwgt_lb
later_weight = others.totalwgt_lb
first_weight.mean(), later_weight.mean()
```

From this output it would seem like first babies are lighter than others by an average of ~0.12 lbs. We then compute the Cohen's d to quantify the effect size of this difference.

```
# Function that computes Cohen's d for 2 given variables
def Cohens_d(group1, group2):

  """Computes Cohen's effect size for two groups.
    
    group1: Series or DataFrame
    group2: Series or DataFrame
    
    returns: float if the arguments are Series;
             Series if the arguments are DataFrames
    """
  diff = group1.mean() - group2.mean()

  var1 = group1.var()
  var2 = group2.var()
  n1, n2 = len(group1), len(group2)

  pooled_var = (n1 * var1 + n2 * var2) / (n1 + n2)
  d = diff / np.sqrt(pooled_var)
  return d

# Computing Cohen's d for first-born and later-born babies
weight_d = Cohens_d(first_weight, later_weight)
```

As per the accepted interpretation thresholds for Cohen's d, the resulting effect size of 0.09 is considered very small (<.2)

To provide a comparison, here are the same computations looking at differences in pregnancy length:

```
# Separate data into first-borns vs all others, assuming we're only interested in live births

first_prglngth = firsts.prglngth
later_prglngth = others.prglngth
first_prglngth.mean(), later_prglngth.mean()
```

This reveals that, on average, first pregnancies are approximately 0.08 weeks longer than other pregnancies. We then compute the effect size for this comparison:

```
length_d = Cohens_d(first_prglngth, later_prglngth)
```

The resulting effect size of -0.03 is even smaller than the one calculated for birthweights. As previously stated, both are considered very small (<0.2).
	
