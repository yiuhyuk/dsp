[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

My Code - 

```python
# Filter dataframes to split between first and other babies
preg = nsfg.ReadFemPreg()
live = preg[preg.outcome == 1]
first = live[live.birthord==1]
other = live[live.birthord!=1]

#live_clean = live[['totalwgt_lb', 'prglngth']].dropna()
#np.corrcoef(live_clean.totalwgt_lb, live_clean.prglngth)

# Function that takes in two vectors and returns the cohen's d
def cohen_d(group1, group2):
    num_group1 = group1.shape[0]
    num_group2 = group2.shape[0]
    mean_group1 = np.mean(group1)
    mean_group2 = np.mean(group2)
    var_group1 = np.var(group1)
    var_group2 = np.var(group2)
    
    pooled_var = (num_group1*var_group1 + num_group2*var_group2)/(num_group1 + num_group2)
    d = (mean_group1 - mean_group2)/pooled_var
    return d

# Calculate and print the cohen's d for first vs. other baby weight and pregnancy length
d_first_other_wgt = cohen_d(first.totalwgt_lb, other.totalwgt_lb)
d_first_other_lngth = cohen_d(first.prglngth, other.prglngth)

print('cohen_d weight: ', '{:.3f}'.format(d_first_other_wgt))
print('cohen_d prengnancy length: ', '{:.3f}'.format(d_first_other_lngth))
```

My Results - 

cohen_d weight:  -0.063
cohen_d prengnancy length:  0.011

First babies on average lighter than other babies (and pregnancies for first babies are longer).  The magnitude of the Cohen's D for weight is greater in absolute terms than it is for prengnancy length.  This means that if we were to observe many such samples, we are more likely to observe that first babies are lighter in those samples than that first pregnancies take longer.
