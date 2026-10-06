# econ3916-lab07-bootstrapping
# Estimation & Bootstrapping — Quantifying Uncertainty Without a Formula

## Objective
I wanted to measure how uncertain my estimates are, first with formulas from the Central Limit Theorem and then with the bootstrap, and to find out when the two approaches agree and when they do not.

## Methodology
- I loaded the UCI Adult Census Income data, which has 32,561 respondents.
- I separated the standard deviation of the data from the standard error of an estimate, and checked the s/sqrt(n) relationship across four sample sizes.
- I built parametric confidence intervals from the CLT and compared how quickly the CLT takes hold for age and for capital gains.
- I ran the bootstrap by hand with my own resampling loop, then repeated it with `scipy.stats.bootstrap`.
- I bootstrapped the median of age and looked into why its standard error came out as zero.
- I compared percentile and BCa bootstrap intervals on a heavily skewed variable.
- I bootstrapped a two-sample difference in mean weekly hours.
- I asked an AI to write a bootstrap-interval function, revised my prompt once, and checked the function against the intervals I had already computed myself.
- I ran a coverage simulation on lognormal data at n=50 to see how often nominal 95% intervals actually contain the true value, for both the mean and the median.

## Key Findings
- The standard deviation describes the spread of the data and stays roughly the same as the sample grows, while the standard error shrinks with sample size, following s/sqrt(n) across the four sample sizes I tried.
- The CLT converges quickly for age but slowly for capital gains, so a normal-based interval is easier to trust for age than for a heavily skewed variable.
- The bootstrap SE of the median of 32,561 whole-number ages is exactly 0.0000. With that many tied values, every resample returns the same median. The bootstrap was not failing here; it was reporting a real property of the data.
- Checking the AI's function against my own results was necessary. My first prompt left out how to handle randomness, so I revised it to add a seed, and only then could I compare its intervals directly with mine.
- In the coverage simulation for the mean, the parametric interval covered [YOUR VALUE]% and the percentile bootstrap covered [YOUR VALUE]%. The gap is inside the Monte Carlo standard error of about 1.3 points, so I cannot tell the two methods apart here, and both under-cover slightly.
- For the median, the mean-centred parametric interval covered only about [YOUR VALUE]%, while the bootstrap stayed near its nominal 95% level. When there is no simple formula for the standard error of a statistic, the bootstrap still gives a usable interval.
