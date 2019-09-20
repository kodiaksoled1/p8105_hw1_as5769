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

*Converting Variables*

When we convert a logical and factor variable into a numeric variable,
we can yield a numeric output for each. However, when we convert a
character variable into a numeric variable, the output shows NA’s. This
explains why we could not take the mean of this variable above. The code
to convert these variables into a numeric variable would look like the
following:

``` r
as.numeric(pull(hw1_pb1_df, vec_factor))
as.numeric(pull(hw1_pb1_df, vec_logical))
as.numeric(pull(hw1_pb1_df, vec_char))
```

Since we just found we can convert a logical vector into a numeric
vector, this allows us to then multiply our random sample by the result:

``` r
#
vec_logical = as.numeric(pull(hw1_pb1_df, vec_logical)) 
vec_logical * (pull(hw1_pb1_df, sample))
```

    ## [1] 0.0000000 0.1315312 0.0000000 0.8867848 0.1169713 0.3186301 0.0000000
    ## [8] 0.7145327

Furthermore, we can also convert the logical vector into a factor
vector. However, a factor vector cannot be multiplied and the output
will again show NA’s. Thus, we cannot multiple the factor vector by our
random sample:

``` r
vec_factor = as.factor(pull(hw1_pb1_df, vec_logical))
vec_factor * (pull(hw1_pb1_df, sample))
```

    ## [1] NA NA NA NA NA NA NA NA

Nonetheless, by converting the logical vector into a factor vector and
then into a numeric vector, now we can multiply the result by our random
sample:

``` r
vec_numeric = as.numeric(vec_factor) 
vec_numeric * (pull(hw1_pb1_df, sample))
```

    ## [1] -0.50219235  0.26306233 -0.07891709  1.77356962  0.23394254  0.63726018
    ## [7] -0.58179068  1.42906542
