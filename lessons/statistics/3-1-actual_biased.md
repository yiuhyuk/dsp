[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

```python
%matplotlib inline

import numpy as np

import nsfg
import first
import thinkstats2
import thinkplot

resp = nsfg.ReadFemResp()

true_mean = np.mean(resp.numkdhh)
pmf = thinkstats2.Pmf(resp.numkdhh, label='actual')

numkd_val_ct = resp.numkdhh.value_counts()

weighted_sum = 0
for i, val in enumerate(numkd_val_ct):
    weighted_sum += i*val
mean_check = weighted_sum/resp.numkdhh.shape[0]

def BiasPmf(pmf, label):
    new_pmf = pmf.Copy(label=label)

    for x, p in pmf.Items():
        new_pmf.Mult(x, x)
        
    new_pmf.Normalize()
    return new_pmf

def get_biased_mean(pmf):
    biased_freq = [i*val for i, val in pmf.Items()]
    observed = [i for i, val in pmf.Items()]
    biased_pmf = [i/sum(biased_freq) for i in biased_freq]
    biased_mean = sum([val*observed[i] for i, val in enumerate(biased_pmf)])
    
    biased_pmf_obj = BiasPmf(pmf, 'biased')
    
    return biased_pmf_obj, biased_mean

biased_pmf, biased_mean = get_biased_mean(pmf)
thinkplot.PrePlot(2)
thinkplot.Pmfs([pmf, biased_pmf])
thinkplot.Config(xlabel='Class size', ylabel='PMF')

print('Actual Mean: ', '{:0.3f}'.format(true_mean))
print('Biased Mean: ', '{:0.3f}'.format(biased_mean))
```

```r
%matplotlib inline

import numpy as np

import nsfg
import first
import thinkstats2
import thinkplot

resp = nsfg.ReadFemResp()

true_mean = np.mean(resp.numkdhh)
pmf = thinkstats2.Pmf(resp.numkdhh, label='actual')

numkd_val_ct = resp.numkdhh.value_counts()

weighted_sum = 0
for i, val in enumerate(numkd_val_ct):
    weighted_sum += i*val
mean_check = weighted_sum/resp.numkdhh.shape[0]

def BiasPmf(pmf, label):
    new_pmf = pmf.Copy(label=label)

    for x, p in pmf.Items():
        new_pmf.Mult(x, x)
        
    new_pmf.Normalize()
    return new_pmf

def get_biased_mean(pmf):
    biased_freq = [i*val for i, val in pmf.Items()]
    observed = [i for i, val in pmf.Items()]
    biased_pmf = [i/sum(biased_freq) for i in biased_freq]
    biased_mean = sum([val*observed[i] for i, val in enumerate(biased_pmf)])
    
    biased_pmf_obj = BiasPmf(pmf, 'biased')
    
    return biased_pmf_obj, biased_mean

biased_pmf, biased_mean = get_biased_mean(pmf)
thinkplot.PrePlot(2)
thinkplot.Pmfs([pmf, biased_pmf])
thinkplot.Config(xlabel='Class size', ylabel='PMF')

print('Actual Mean: ', '{:0.3f}'.format(true_mean))
print('Biased Mean: ', '{:0.3f}'.format(biased_mean))
```
