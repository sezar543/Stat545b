Assignment 1-B
================

**Deadline**: Saturday, November 7, 2020 at 23:59 PST

**Total Points**: 20

This assignment first covers making a function (Exercise 1, covered in
Week 1), then using list columns (Exercise 2, covered in Week 2) to
explore a data set.

-   [ ] For your convenience, we’ve indicated all action items with a
    checkbox, like so.

## Setup

1.  [ ] Go to canvas to get your invitation to the STAT 545 homework
    GitHub Organization. You can find this in the description of
    Assignment 1-B.
2.  [ ] Work within your `assignment-1b` folder in your new repository,
    and complete the assignment by filling in this very .Rmd file. Your
    repo will be seeded with instructions for this milestone. Commit and
    push your work early and often (although this will not be graded,
    many students end up in situations where they wish they pushed more
    frequently).

## Tidy Submission (2 points)

Follow these steps to submit your work. Be sure to familiarize yourself
with the rubric for a tidy submission below, before doing these steps.

1.  [ ] Make a README file in your `assignment-1b` folder. It should let
    a visitor know what’s in this folder.
2.  [ ] Make/update a main README file for your entire repository. It
    should orient a visitor to what this repository *is*, and that
    visitor should know how to engage with the repository. There should
    not be much here.
3.  [ ] Make your assignment appear nicely rendered and viewable online,
    such as by changing the output to `output: github_document` in the
    YAML header.
    -   You could also use GitHub pages. But, the assignment needs to
        correspond to the tagged release, and we still need to be able
        to navigate to your repository somehow.
4.  [ ] Tag a release in your GitHub repository corresponding to your
    submission before the deadline.
    -   Forgotten how to tag a release? We have instructions at the
        bottom of the [Collaborative Milestone 1
        repo](https://stat545.stat.ubc.ca/collaborative-project/milestone1/readme/)
        from STAT 545A.
5.  [ ] Grab the URL corresponding to your viewable output from Step 3,
    and submit that to canvas. Also, please let us know what you thought
    of this assignment – any feedback would be appreciated.

**Rubric**:

-   The above steps were followed.
-   Your work is self-contained in the `assignment-1b` folder.
-   Your work must be reproducible from beginning to end. That is, a
    member of the teaching team should be able to run all code
    error-free and reproduce the output files.
-   You use proper English, spelling, and grammar, and write concisely.
    If there’s any uncertainty in determining a grade here, the [UBC MDS
    writing
    rubric](https://github.com/UBC-MDS/public/blob/master/rubric/rubric_writing.md)
    will be referred to.
-   If there’s any further uncertainty in determining a grade for this
    tidy submission portion, the [UBC MDS mechanics
    rubric](https://github.com/UBC-MDS/public/blob/master/rubric/rubric_mech.md)
    will be referred to.

``` r
#install.packages("palmerpenguins")
#install.packages("lubridate")
#install.packages("gapminder")
# install.packages("tidyverse")
#install.packages("testthat")
```

``` r
suppressPackageStartupMessages(library(palmerpenguins))
suppressPackageStartupMessages(library(lubridate))
suppressPackageStartupMessages(library(gapminder))
```

    ## Warning: package 'gapminder' was built under R version 4.1.3

    ## Warning: replacing previous import 'lifecycle::last_warnings' by
    ## 'rlang::last_warnings' when loading 'tibble'

    ## Warning: replacing previous import 'lifecycle::last_warnings' by
    ## 'rlang::last_warnings' when loading 'pillar'

``` r
suppressPackageStartupMessages(library(tidyverse))
```

    ## Warning: replacing previous import 'lifecycle::last_warnings' by
    ## 'rlang::last_warnings' when loading 'hms'

``` r
suppressPackageStartupMessages(library(testthat))
```

## Exercise 1: Functions (10 points)

In this exercise, you’ll be making a function and fortifying it. The
function need not be complicated. The function need not be “serious”,
but shouldn’t be nonsense.

**Function Ideas**

Basic:

-   Did you repeat any code for a data analysis in STAT 545A? If so,
    consider making a function for this action.
-   Write a *wrapper* around an existing function.
    -   For example, perhaps accepting a narrower range of inputs (like
        not allowing logical vectors), or providing a different output.
    -   A specific example: my [`rqdist()`
        function](https://github.com/vincenzocoia/rqdist/blob/master/R/rqdist.R#L1)
        is a wrapper around `quantreg::rq()`, narrowing its
        functionality.
    -   It’s usually better to narrow a function’s focus than to
        broaden, so that a function doesn’t end up doing too much.
-   Make a function extracting parts of an `"lm"` object that you can’t
    easily access (`broom` aside), or measuring the “difference” between
    a linear and quadratic fit.
-   Make a special plot that you’d want to repeat when exploring your
    data.
-   You might find a function useful to apply for Exercise 2.

Advanced:

-   Make a new ggplot2 geom. Need inspiration? Fun ideas count –
    [`geom_lime()` and
    `geom_pint()`](https://github.com/coolbutuseless/geomlime) are great
    examples (thanks, Asfar, for finding this) – but it’s not enough to
    make something like `geom_parrot()` based on these functions,
    because there’s not enough original work to answer the questions we
    have for you.
-   Fit a Beverton-Holt model (or some other scientifically motivated
    parametric function) to some data via least squares or some other
    method.
-   [Create your own `broom` tidier
    function](https://www.tidymodels.org/learn/develop/broom/) for a
    model that’s currently incompatible with `broom` (warning: this uses
    S3 object oriented programming, but you don’t need to implement that
    for this assignment).

**Caveats**

The first three caveats are prone to a penalty of -1 point.

-   **Other sources**: We need to see your own work here. You *can* use
    someone’s function as inspiration for your function, just be sure
    to (1) reference the source of inspiration for your function,
    and (2) you should be able to answer the questions in this Exercise
    for your own work.
-   **Too simple**: Your function should involve more than just a
    calculation that you can do with operations like `+`, `-`, `*`, `/`,
    `&`, `<`, etc. – even with simple functions like `sqrt()` that have
    one argument only. But, add a feature like `trim` (as in the
    `mean()` function, if it makes sense to do so), and you have
    something that’s no longer simple. So, `function(x) x ^ 2` is too
    simple. But, `function(x) max(x) - min(x)` isn’t too simple, because
    the `max()` and `min()` functions have another option (`na.rm`).
-   **Nonsense**: The function should be sensible. Example of a nonsense
    function: `function(x, y) x ^ (x + y) + x / y ^ x - 1`.
-   **Making more than one function**: You might encounter this
    situation if a task is too big for one function, and you just
    wouldn’t be satisfied with yourself if you only made one function.
    If so, it sounds like you’re well on your way to making an R package
    in Week 3 (Assignment 2-B), so definitely keep the idea. We’ll only
    be grading one function for this assignment though, so if you make
    more than one, please let us know which one you’d like to be graded.

### 1.1 Documentation and Design (5)

| Rubric        | Description                                                                                      | Points |
|---------------|--------------------------------------------------------------------------------------------------|--------|
| Documentation | Documentation is complete, according to the instructions.                                        | 1      |
| Focussed      | Your function doesn’t do too many actions – it does one thing, as described in your description. | 1      |
| Generalised   | *See below*                                                                                      | 2      |
| Format        | *See below*                                                                                      | 1      |

In the space below, document your function:

-   [ ] **Description**: In 1-2 brief sentences, describe what the
    function does.
    -   As a model answer, check out the “Description” section (the very
        first section) in the documentation of an R function that you
        know and love.
    -   Technical language is OK (like “Generalised Linear Model”), but
        not a step-by-step written account of each line. If you feel the
        need to add more details, separate these details from the main
        description. In fact, many functions have a “Details” section in
        their documentation! Just check out `lm()` as an example – but
        don’t go overboard like that.
-   [ ] For each **argument**,
    -   [ ] Write the argument name.
    -   [ ] Describe the input: What restrictions are there – should it
        be a vector? A list? A specific type of vector, like numeric? If
        there’s a default value, specify what the default is.
    -   [ ] Briefly justify (1-2 sentences) your choice of name and (if
        applicable) default value.
-   [ ] For the **output**:
    -   [ ] Describe the object that’s returned. Is it a vector? A list?
        Is it a numeric vector? What does the object represent?
    -   [ ] Briefly justify (1-2 sentences) your choice of output
        format.

Here’s an elaboration on the rubrics:

**Generalised**

Your function should not be specific to a decision that you made for an
analysis. Use function arguments to accomplish being able to use this
function in other analyses. The following examples are signs that you
need to use more arguments to generalise your function:

-   Your function should not rely on anything from your working
    environment.
-   Your function should not rely on “magic numbers” – pre-selected
    numbers (or options) that appear inside the function that can’t be
    accessed by a user of the function.
    -   For example, maybe `quantile(x, type = 1, ...)` appears in your
        function. The choice of 1 is arbitrary.
    -   That is, it’s arbitrary *unless* it’s specific to your function
        – `type = 1` corresponds to the empirical quantile, and this
        would be fine if your function is *designed* to calculate the
        empirical quantile.

Adding additional arguments sometimes means you’ll have to think outside
of the box as to how you’ll design your function, but that’s the fun
part.

-   At least three of the below are relevant/appropriate, and therefore
    found in your function (if not, your function may be too simple):
    -   Appropriate `NA` handling, such as with `na.rm`, if relevant
        (usually relevant for *summarising* functions that would appear
        in `dplyr::summarise()` – typically not in vectorized functions
        that would appear in `dplyr::mutate()`).
    -   Appropriate defaults are used, if relevant. (Your justification
        is considered here).
    -   The ellipsis (`...`) is used as an “argument”, if
        relevant/appropriate.
    -   A “special option” is included, to tweak the function’s
        behaviour. For example, the `trim` argument in the `mean()`
        function, or `type` in the `quantile()` function. Including this
        doesn’t count if this argument should be absorbed by the
        ellipsis (can’t double-dip the use of ellipsis and this option)
    -   A second special option is included.

**Format**

What we’re looking for in terms of the **format** of the input and
output:

-   Arguments have appropriate names (you should at least have sound
    justification).
-   Input should not take a rigid form. An example that’s too rigid is a
    data frame that’s expected to have special types of columns.  
-   The output is consistent – for example, always gives a list. An
    example of inconsistent output: `sapply(1:3, seq_len)` gives a list,
    and `sapply(1:3, sqrt)` gives an (atomic) vector.
-   The structure of the input and output makes sense. Sometimes the
    input and output is a natural choice (as in the `sqrt()` function),
    and other times it’s not (as in the `lm()` function).
-   You’ve made use of data masking when it makes sense to do so, and
    used curly-curly (`{{ var }}`) in your function code.

------------------------------------------------------------------------

<!----------- Documentation goes here ---------------------->

**Description**

The function lin_indep_threevectors takes three numeric vectors of the
same length as input and check if they are linearly independent or
dependent. If they are liearnly dependent, the function returns true
otherwise false.

-   We expect the entires of vectors to be numeric.
-   Sine R computes the determinant of a matrix using approximation, we
    cannot check if determinant is zero or not. Therefore this function
    works if the non-zero entries of three vectors are bigger than
    10^(-5)

**Input (Arguments)**

-   `x`: first vector

    -   *Justification*: since these are just vectors, I use the natural
        convention in math books for vectors, i.e. namely x, y, z,….

-   `y`: second vector

-   `z`: third vector

-   verbose

**Output**

Outiput is a boolean true/false.

<!---------------------------------------------------------->

------------------------------------------------------------------------

### 1.2 Write the Function (3)

| Rubric   | Description                                                                  | Points |
|----------|------------------------------------------------------------------------------|--------|
| Accuracy | Does your function do what you intended it to do, as per your documentation? | 2      |
| Messages | Are your messages well-placed in the function, and informative?              | 1      |

-   [ ] Write your function in the space below, in a code chunk.
-   [ ] Implement at least one of these two message-bearing methods,
    using conditionals (`if` statements) to do so:
    -   Add useful error messages or warnings: use the `stop()` or
        `warning()` function in an `if` statement. Ensure the message is
        informative. In one or two brief sentences: Why did you choose
        what you chose – i.e., warning or stop?
    -   Add a `verbose` argument (counts as a “special argument” in
        1.2), taking a logical input, that keeps the user up-to-date
        with messages that print to screen as the function is running.
        This is mostly relevant for functions that could take a long
        time to run, but for this assignment, it’s OK for any multi-line
        function.

<!------------ Write your function below here -------------->

``` r
# x, y, z are three vectors of the same length.
# verbose is a logical argument. If True, it prints the rows of the matrix matrix(x,y,z) that is chosen in the for loop to check if the determinant of the corresponding sub-matrix of size 3x3 is zero.
# sine R computes the determinant of a matrix using approximation, we cannot check if determinant is zero or not. Therefore this function works if the non-zero entries of three vectors are bigger than 10^(-5) .

lin_indep_threevectors <- function(x, y, z, verbose=FALSE, na.rm = FALSE) {
  if(!is.numeric(x)||!is.numeric(y)||!is.numeric(z)) {
    stop('The entries of vectors are not numeric.\n',
         'You have provided an object of class: ',class(c(x,y,z))[1])
    }
  
  if( length (x) - length (y) !=0 || ( length(x) - length (z) ) !=0){
    stop('The length of these vectors are not equal and so, it does not make sense to check if they are linearly independent!')
  }
  
  n <- length (x)
  A <- matrix( 
     c(x,y,z), # the data elements 
     nrow=n,              # number of rows 
     ncol=3,              # number of columns 
     byrow = FALSE)        # fill matrix by rows

  for(i in 1:(n-2)){
    for(j in (i+1):(n-1)){
      for(k in (j+1):n){
         B <- A[c(i,j,k),c(1,2,3)]
         if (verbose==TRUE){
             cat("Computing the determinant of the 3-by-3 submatrix of rows ",i,j,k,"\n")
             #cat("j=",j,"\n")
             #cat("k=",k,"\n")
         }
      
         if( abs(det ( B )) > 1e-15 ) {
             cat("These three vectors are linearly independent\n");
             return (TRUE)
         }
      }
    }
  }
  cat("These three vectors are linearly dependent.\n")
  return (FALSE)
}
```

<!---------------------------------------------------------->

### 1.3 Test the Function (2 points)

| Rubric | Description                                                                                      | Points |
|--------|--------------------------------------------------------------------------------------------------|--------|
| Choice | Your demonstrations aren’t redundant; neither are the tests; selected inputs are useful to check | 2      |

-   [ ] Demonstrate the use of your function, using at least two
    non-redundant inputs.
-   [ ] Write formal tests for your function. You should use at least
    three non-redundant uses of an `expect_()` function from the
    `testthat` package, and they should be contained in a `test_that()`
    function (or more than one).

Example of non-redundant inputs:

-   Vector with no NA’s
-   Vector that has NA’s
-   Vector of a different type (if relevant)
-   Vector of length 0, like `numeric(0)`.

Example of redundant inputs:

-   Each providing a different number (unless one of these numbers have
    some significance, like a limit point – just tell us if that’s the
    case)

<!------------ Test your function below here --------------->

``` r
Answer <- test_that("Testing lin_indep_threevectors", {
  # Check if the functions gives an error if one of the vectors is not numeric.
  expect_error(lin_indep_threevectors(c(2, 1,1),c(3,2,1),c("A","B","C")))
  
  # Check if the functions returns true if the vectors are linearly independent.
  expect_true(lin_indep_threevectors(c(2,1,1),c(3,2,1),c(5,5,6)))
  
  # Check if the functions returns false if the vectors are not linearly independent.
  expect_false(lin_indep_threevectors(c(2,1,1,1),c(1,0,0,0),c(4,1,1,1)))
  
  # Check if the functions gives an error if the length of the three vectors are not all equal.
  expect_error(lin_indep_threevectors(c(2,1,1,1),c(1,0,0,0),c(4,1,1,1,1)))
})
```

    ## These three vectors are linearly independent
    ## These three vectors are linearly dependent.
    ## Test passed

<!---------------------------------------------------------->

### 1.4 (**Optional**, 1 bonus point)

Contribute to an open-source R package on GitHub by making an
improvement to one of their functions, or perhaps even adding your
function to their package. If you’re nervous, maybe ask the developers
first via a GitHub Issue or email (check their `CONTRIBUTING` file for
more details, if they have one).

Note: You can’t get above 100% on this assignment.

If you choose to do this, just put a link to the pull request that you
made on the R package’s GitHub repository. Your pull request doesn’t
need to be accepted by the developers, but your pull request *should* be
realistic in order to get this bonus point.

**You can even do this after you submit the assignment**. For example,
you might want to wait until we learn about R packages before you do
this. If this is the case, just make sure to let your grader know once
you submit your pull request, via a GitHub Issue in your homework
repository (don’t forget to `@tag` them!), also including a link to your
pull request. But, you have until the deadline of Assignment 5-B to do
this, and you only get one attempt!

## Exercise 2: List Columns (8 points)

### 2.1 (8 points)

| Rubric      | Description                                             | Points |
|-------------|---------------------------------------------------------|--------|
| First map   | First `purrr` mapping function was used correctly       | 2      |
| Second map  | Second `purrr` mapping function was used correctly      | 2      |
| (Un)nesting | Was done appropriately                                  | 2      |
| Explanation | What was claimed to be calculated was indeed calculated | 2      |

For this exercise, you’ll be evaluating a model that’s fit separately
for each group in some dataset.

Examples:

-   Maybe your model is a linear model (using `lm()`) for each continent
    in the `gapminder::gapminder` dataset.
-   Maybe your model is a distribution of a single variable (using the
    [`distplyr` package](https://distplyr.netlify.app/)) for each
    penguin in the `palmerpenguins::penguins` dataset.

Your tasks are as follows.

1.  [ ] Make a column of model objects. Do this using the appropriate
    mapping function from the `purrr` package. Note: it’s possible
    you’ll have to make use of nesting, here.
    -   For `distplyr`, use a `distplyr::dst_*()` function of your
        choosing, like `dst_norm()` or `dst_step()`. Note that there
        aren’t that many `dst_*()` functions yet, sorry – `distplyr` is
        still quite young.
2.  [ ] Evaluate the model in a way that interests you. But, you should
    evaluate something other than a single number for each group. Hint:
    you’ll need to use another `purrr` mapping function again.
    -   For `distplyr`, use a distributional representation of your
        choosing, such as quantiles, using the appropriate
        `distplyr::enframe_*()` function.
3.  [ ] Print out the tibble so far.
4.  [ ] Unnest the resulting calculations, and print your final tibble
    to screen. Make sure your tibble makes sense: column names are
    appropriate, and you’ve gotten rid of columns that no longer make
    sense.
5.  [ ] Don’t just blindly do this exercise: in 1-2 brief sentences,
    tell us what you’ve just calculated, and in what column.

<!------------ Put your work here -------------------------->

``` r
#devtools::install_github("vincenzocoia/distplyr")
library('distplyr')
```

    ## Loading required package: distionary

``` r
ExerTwo1 <- gapminder %>% 
  select(continent, year, pop) %>% 
  nest(data = c(pop, year)) %>%
  mutate(model = map(data, ~ lm(year ~ log(pop), data = .x))) 

ExerTwo1$model[[1]]
```

    ## 
    ## Call:
    ## lm(formula = year ~ log(pop), data = .x)
    ## 
    ## Coefficients:
    ## (Intercept)     log(pop)  
    ##    1944.650        2.119

``` r
(ExerTwo2 <-ExerTwo1 %>%
  unnest(data)   %>% 
    group_by(continent) %>% 
    summarise(mean_pop = mean(pop, na.rm = TRUE),
            var_pop  = var(pop, na.rm = TRUE), .groups = 'drop') %>% 
    mutate(quantile = map2(mean_pop, var_pop, dst_norm) %>% 
             map_dbl(eval_quantile, at = 0.975))
)
```

    ## # A tibble: 5 x 4
    ##   continent  mean_pop var_pop   quantile
    ##   <fct>         <dbl>   <dbl>      <dbl>
    ## 1 Africa     9916003. 2.40e14  40277655.
    ## 2 Americas  24504795. 2.60e15 124422642.
    ## 3 Asia      77038722. 4.28e16 482526272.
    ## 4 Europe    17169765. 4.21e14  57387124.
    ## 5 Oceania    8874672. 4.23e13  21626869.

In tibble ExerTwo1, I computed the linear regression model betweenthe
variables year and log(pop). In tibble ExerTwo2, I unnest the columns
year and pop, then I computed mean and variance in each continent, and
then I computed the 0.975 quantile.

<!---------------------------------------------------------->

### 2.2 (**Optional**, 1 bonus point)

Choose one of the following. Following a linear model fit to groups on
the gapminder dataset, either:

-   Find countries with interesting stories. Sudden, substantial
    departures from the temporal trend is interesting. How could you
    operationalize this notion of “interesting”?
-   Use the residuals to detect countries where your model is a terrible
    fit. Examples: Are there 1 or more freakishly large residuals, in an
    absolute sense or relative to some estimate of background
    variability? Are there strong patterns in the sign of the residuals?
    E.g., all positive, then all negative, then positive again.
-   Fit a regression using ordinary least squares and a robust
    technique. Determine the difference in estimated parameters under
    the two approaches. If it is large, consider that country
    “interesting”.
