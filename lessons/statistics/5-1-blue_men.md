[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

```python
from scipy.stats import norm
# 5'10" = 177.8cm and 6'1" = 185.42
prob_blue = norm.cdf(x=185.42, loc=178, scale=7.7) - norm.cdf(x=177.8, loc=178, scale=7.7)
print('The probability of being eligible is :', '{:0.3f}'.format(prob_blue))
```

The probability of being eligible is: 0.343

I just took the probability that people are shorter than 6'1 and subtracted the probability that people are shorter than 5'10.  The difference is the probability that a randomly sampled male will be between 5'10 and 6'1.
