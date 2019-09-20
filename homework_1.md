Homework 1
================
Kodiak Soled
9/20/2019

**Problem 1**

*Creating a Dataframe*

The following dataframe is comprised of a random sample size of 8 from a
standard normal distribution, a logical vector whose elements of the
sample are greater than 0, a character vector of length 8, and a factor
vector of length 8 with 3 different factor “levels”:

``` r
set.seed(100)
hw1_pb1_df = tibble(
  sample = rnorm(8, mean = 0, sd = 1), 
  vec_logical = c(sample > 0),
  vec_char = c("one", "two", "three", "four", "five", "six", "seven", "eight"),
  vec_factor = factor(c("low", "low", "low", "med", "med", "med", "high", "high"))
)
```

*Taking the Mean of Variables*

We can take the mean of the numeric vector (i.e., sample) and the
logical vector (i.e., vec\_logical) from the above dataframe using the
following code:

``` r
mean_samp = mean(pull(hw1_pb1_df, sample))
mean_vec_logical = mean(pull(hw1_pb1_df, vec_logical))
```

From this code, we can find:

  - The mean of the sample is 0.1256937.

  - The mean of the vec\_logical is 0.625.

However, if we try to take the mean of a character (i.e., vec\_char) or
factor (i.e., vec\_factor) vector, R will present a warning output
stating that this function is not possible. This code would look like
the following:

``` r
mean_vec_char = mean(pull(hw1_pb1_df, vec_char))
mean_vec_factor = mean(pull(hw1_pb1_df, vec_factor))
```
