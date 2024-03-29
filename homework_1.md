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

**HW Problem 2**

*Creating a Dataframe*

This second dataframe is comprised of two random samples (x and y) of
size 500 from a standard normal distribution, a logical vector that
indicates whether x + y \> 1, and the coerced numeric and factor vectors
of the previous logical vector:

``` r
set.seed(100)
hw1_pb2_df = tibble(
  x = rnorm(500, mean = 0, sd = 1),
  y = rnorm(500, mean = 0, sd = 1),
  vec_logical = c(x + y > 1),
  vec_numeric = as.numeric(vec_logical),
  vec_factor = as.factor(vec_logical)
)
```

*Describing the Dataframe*

  - The dataset has 2500 variables (500 rows and 5 columns).
  - The mean of x is -0.0376074.
  - The median of x is -0.0600876.
  - The standard deviation of x is 1.0049216.
  - The proportion of cases where x + y \> 1 is 0.242.

The code that was used to find the above attributes about the second
dataframe is as follows:

``` r
nrow(hw1_pb2_df)*ncol(hw1_pb2_df)
mean(pull(hw1_pb2_df, x))
median(pull(hw1_pb2_df, x))
sd(pull(hw1_pb2_df, x))
sum(pull(hw1_pb2_df, vec_logical), na.rm=TRUE)/500
```

*Making Scatterplots of the Dataframe*

Below is a scatterplot of our two random samples x and y. The logical
variable is colored with teal to indicate values where x + y \> 1 and
peach to indicate values where x + y \<=
1:

``` r
ggplot(hw1_pb2_df, aes(x = x, y = y, color = vec_logical)) + geom_point()
```

![](homework_1_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

I will now export this scatterplot to my project directory using the
following code:

``` r
ggsave("hw1_pb2_df.pdf", width = 4, height = 6)
```

This next scatterplot of our two random samples x and y is colored with
a gradient of black to blue to represent the continuous nature of a
numeric
variable:

``` r
ggplot(hw1_pb2_df, aes(x = x, y = y, color = vec_numeric)) + geom_point()
```

![](homework_1_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

This last scatterplot of our two random samples x and y is similarly
colored in the same fashion as the first scatterplot as a factor
variable similarly uses categories to indicate which values are x + y \>
1 and which values are x + y \<= 1:

``` r
ggplot(hw1_pb2_df, aes(x = x, y = y, color = vec_factor)) + geom_point()
```

![](homework_1_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

*Comment on Color Scales*

In summary, the three scatterplot’s color scales represent the type of
variable in each respective scatterplot. Thus, the first and third
scatterplots (vec\_factor and vec\_logical) have two distinct colors
that represents categorical data within a factor and logical vector. The
second scatterplot (vec\_numeric) has a gradient which represents
continuous data of a numeric vector
