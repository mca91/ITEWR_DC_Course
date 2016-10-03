---
title       : OLS Basics 
description : This section contains exercises dealing with the simple linear regression model and estimation using ordinary least squares. 
attachments :
  slides_link : https://github.com/Emwikts1970/URFITE_DC/raw/master/Econometrics

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:35167f113b
## Violation of OLS Assumptions

Have a look at the plot that showed up in the viewer to the right. Which of the OLS assumptions could be possibly violated?

*** =instructions
- No perfect multicollinearity
- Homoskedasticity
- Outliers are seldom
- Y is $\chi^2_{11}$ distributed

*** =hint
Have a look at the plot. What can you say about the dispersion of observations?

*** =pre_exercise_code
```{r}
library(sandwich)

set.seed(1)
x <- runif(500, 0, 1)
y <- 5 * rnorm(500, x, x)
plot(y ~ x, col = "steelblue", pch = 19)
```

*** =sct
```{r}
msg_bad <- "That is not correct!"
msg_success <- "Exactly! There seems to be heteroskedasticity: Dispersion increases with x."
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_success, msg_bad, msg_bad))
```

--- type:NormalExercise lang:r xp: skills: key:9d4515394d
## Regression I: Class Size and Test Score

A researcher wants to analyse the relationship between class size and pupils' average test score. Therefore he measures both variables in 10 different classes obtaining the following results:

  <table>
      <tr>
        <td><b>Class Size</b></td>
        <td>23</td>
        <td>19</td>
        <td>30</td>
        <td>22</td>
        <td>23</td>
        <td>29</td>
        <td>35</td>
        <td>36</td>
        <td>33</td>
        <td>25</td>
      </tr>
      <tr>
        <td><b>Test Score</b></td>
        <td>430</td>
        <td>430</td>
        <td>333</td>
        <td>410</td>
        <td>390</td>
        <td>377</td>
        <td>325</td>
        <td>310</td>
        <td>328</td>
        <td>375</td>
      </tr>
    </table>


*** =instructions

- Create vectors, `cs` for class sizes and `ts` for test scores, containing the results
- Draw a scatter plot of the results using `plot`
- Compute mean, median and variance and standard deviation of test scores. Use existing R functions!
- Compute both the covariance and pearson's correlation coefficient for `cs` and `ts` using R functions
- Estimate a linear regression of test score on class size using `lm()`. Store the result in `mod`
- `mod` is an object of type `list` with named entries. Check this using the function `is.list()`
- See what information you can obtain from `mod` using the `$` operator. Read out an arbitrary entry of `mod` 


*** =hint



*** =sample_code
```{r}
# Create both vectors


# Draw the scatter plot


# Compute mean, median, variance & standard deviation of test score


# Compute the covariance and the correlation coefficient


# Estimate the regression model and store it in mod


# Check that mod is an object of type list 


# Read out some arbitrary entry of mod using $


```

*** =solution
```{r}
# Create both vectors
cs <- c(23, 19, 30, 22, 23, 29, 35, 36, 33, 25)
ts <- c(430, 430, 333, 410, 390, 377, 325, 310, 328, 375)

# Draw the scatter plot
plot(cs,ts)

# Compute mean, median, variance & standard deviation of test score
mean(ts)
median(ts)
var(ts)
sd(ts)

# Compute the covariance and the correlation coefficient
cov(cs,ts)
cor(cs,ts)

# Estimate the regression model and store it in mod
mod <- lm(ts ~ cs)

# Check that mod is an object of type list 
is.list(mod)

# Read out some arbitrary entry of mod using. E.g. fitted values:
mod$fitted.values

```

*** =sct
```{r}
test_object("cs")
test_object("ts")

test_function("plot")

test_function("mean")
test_function("median")
test_function("var")
test_function("sd")
test_function("cov")
test_function("cor")

test_or(
  test_function("lm", eq_condition = "equal", not_called_msg = "You didn't call `lm()`!",
              incorrect_msg = "You didn't call `lm()` with the correct argument, `formula`."),
  test_function("lm", eq_condition = "equivalent", not_called_msg = "You didn't call `lm()`!",
              incorrect_msg = "You didn't call `lm()` with the correct argument, `formula`.")
)

test_object("mod")

test_function("is.list", args="x")

test_student_typed("mod$")

```

--- type:NormalExercise lang:r xp: skills: key:6e64f67c78
## Regression II: Class Size and Test Score

Consider again the relation of class size and test score. The model object `mod` from the previous exercise is available in your workspace. This means you can use it for subsequent tasks. Convince yourself by typing `summary(mod)` in to the console and get yet again detailed information on the estimated model!



*** =instructions

- Obtain an overview over the model object `mod` using `summary()`
- Add the regression line to the scatterplot. Hint: use `abline()`
- Store the regression summary into `summary`. Discover what information you can extract from `summary` by use of the `$` operator
- Suppose you are interested in how good the model fits the data. Create a new variable `R2` storing the regression's $R^2$
- You can extract a named $2\times4$ matrix with, amongst other things, estimated coefficients and standard errors. Save this matrix to an object named `coef`

*** =hint

*** =pre_exercise_code
```{r}
cs <- c(23, 19, 30, 22, 23, 29, 35, 36, 33, 25)
ts <- c(430, 430, 333, 410, 390, 377, 325, 310, 328, 375)
mod <- lm(ts ~ cs)
```

*** =sample_code
```{r}
# Use summary() the get an overview over your model


# Add the regression line the the scatterplot
plot(cs,ts)

# Store summary(mod) into summary


# Store the regression's R^2 in R2


# Save the coefficient matrix to coef
```

*** =solution
```{r}
# Use summary() the get an overview over your model
summary(mod)

# Add the regression line the the scatterplot
plot(cs,ts)
abline(mod)

# Store summary(mod) into summary
summary <- summary(mod)

# Store the regression's R^2 in R2
R2 <- summary$r.squared

# Save the coefficient matrix to coef
coef <- summary$coefficients

```

*** =sct
```{r}
test_predefined_objects("mod")
test_function("summary")
test_function("abline")
test_object("summary")
test_object("R2")
test_object("coef")

```

--- type:NormalExercise lang:r xp: skills: key:449f4c19de
## Regression III: Class Size and Test Score 

So far, You have conducted regressions where the model consisted of an intercept and another regressor. In this exercise you will learn ways to specify and to 
estimate regression models without the intercept and how to conduct regression on a constant.

*Vectors `cs` and `ts` as well as the list object `mod` from previous exercises are availabe in your working environment.*


*** =instructions

- Use the help function on `lm` (`?lm`) to find out how to specify a `formula` for a regression of `ts` solely on `cs`, i.e. a regression witouh intercept
- Estimate the regression model without intercept and store it in `mod_ni`
- Convince yourself that everything went right. Extract the coefficient matrix from the models summary and store it to `coef`
- Plot both regression lines

*** =hint

- In `lm()` use `ts ~ cs - 1` as the `formula` argument to estimate a regession model lacking an intercept

*** =pre_exercise_code
```{r}
cs <- c(23, 19, 30, 22, 23, 29, 35, 36, 33, 25)
ts <- c(430, 430, 333, 410, 390, 377, 325, 310, 328, 375)
mod <- lm(ts ~ cs)
```

*** =sample_code
```{r}
# Regress ts solely and cs, sore it to mod_ni


# Extract the coefficient matrix from the models summary, save it to coef


# Plot regression lines for both models
plot(cs,ts)

```

*** =solution
```{r}
# Regress ts solely and cs, sore it to mod_ni
mod_ni <- lm(ts ~ cs - 1)

# Extract the coefficient matrix from the models summary, save it to coef
coef <- summary(mod_ni)$coefficients

# Plot regression lines for both models
plot(cs,ts)
abline(mod)
abline(mod_ni)

```

*** =sct
```{r}
test_predefined_objects("mod")

test_correct(test_function("lm"),
    {
    test_or(
        test_student_typed("ts ~ cs - 1"),
        test_student_typed("ts ~ cs + 0")
    }
)

test_function("lm")

test_object("mod_ni", eval=F)
test_object("coef")

test_function("abline", index=1)
test_function("abline", index=2)

```

--- type:NormalExercise lang:r xp:100 skills:1 key:d71e82b5ef
## Regression and Robust Standard Errors

In the previous exercise, you saw example data exhibiting heteroskedasticity. In this exercise, we'll have a look at how 
we can get a regression summary reporting robust standard errors.

A data set consisting of observations you have seen before is now available in the workspace.

*** =instructions
- Regress `y` on `x` and a constant. Store the result in `mod`
- Report coefficients and robust standard errors.
- Plot the regression line.

*** =hint
- Use `lm()` for the first instruction.
- Use the `coeftest()` function. See how you can specify a robust variance-covariance estimator to be used. coeftest has an argument were this can be specified. A look at the help file might be useful: `?coeftest`.
- For the plot, use `abline()` on your model object.

*** =pre_exercise_code
```{r}
library(sandwich)
library(AER)
set.seed(1)
x <- runif(500, 0, 1)
y <- 5 * rnorm(500, x, x)
```

*** =sample_code
```{r}
# Data vectors `x` and `y` are now available in your workspace.


# Regress y on x. Store the model in `mod`.


# Report coefficients and robust standard errors.


# Add the regression line to the plot created by the code below.
plot(y ~ x, col = "steelblue", pch = 19)


```

*** =solution
```{r}
# Data vectors `x` and `y` are now available in your workspace.


# Regress y on x. Store the model in `mod`.
mod <- lm(y~x)

# Report coefficients and robust standard errors.
coeftest(mod, vcov.=vcovHC(mod, type="HC0"))

# Add the regression line to the plot created by the code below.
plot(y ~ x, col = "steelblue", pch = 19)
abline(mod)
```

*** =sct
```{r}
test_function("lm", args = "formula",
              not_called_msg = "You didn't call `lm()`!",
              incorrect_msg = "You didn't call `lm()` with the correct argument, `formula`.")

test_object("mod")

test_function("coeftest", args = c("x","vcov."))
test_function("abline")


test_error()

success_msg("Good work!")
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:13d4cf0fb6
## Interpreting OLS Regressions I

Suppose that a researcher, using data on class size ($CS$) and average test score ($TestScore$) from 50 third-grade classes, estimates the OLS regression:

$$ \widehat{TestScore} = 640.3 - 4.93 \times CS, R^2 = 0.11, SER= 8.7 $$

<i>Say a class room has 25 students. What is the regression's prediction for that classroom's average test score? Don't forget: You can use the R console as a calculator!</i>

*** =instructions

- 517.05
- 1337
- 0
- 1

*** =hint

Have a look at the regression equation. How can you interpret the relation on the right hand side?

*** =sct
```{r}
msg_bad <- "That is not correct!"
msg_success <- "Exactly!"
msg_joke <- "LoL, your definitely not 1337!"
test_mc(correct = 1, feedback_msgs = c(msg_success, msg_joke, msg_bad, msg_bad))
```

--- type:NormalExercise lang:r xp:50 skills:1 key:b0b7650bb3
## Interpreting OLS Regressions II

Suppose that a researcher, using data on class size $CS$ and average test scores from 50 third-grade classes, estimates the OLS regression:

$$ \widehat{TestScore} = 640.3 - 4.93 \times CS, R^2 = 0.11, SER= 8.7 $$

*** =instructions
Last year a classroom had 21 students, and this year it has 24 students. What is the regression's prediction for the change in the classrom average test score?

*** =hint

Have a look at the regression equation. How can you interpret the relation on the right hand side? What does this imply if you got test scores for two different class sizes?

*** =sample_code
```{}
# What is the difference in average test score?


```

*** =solution
```{r}
# What is the difference in average test score?
(640.3 - 4.93 * 24) - (640.3 - 4.93 * 21)

```

*** =sct
```{r}
test_output_contains("(640.3-4.93*24) - (640.3-4.93*21)", incorrect_msg = "No, that is not correct...")
```

--- type:NormalExercise lang:r xp:50 skills:1 key:250d5774a4
## Interpreting OLS Regressions III

Suppose that a researcher, using data on class size $CS$ and average test scores from 50 third-grade classes, estimates the OLS regression:

$$ \widehat{TestScore} = 640.3 - 4.93 \times CS, R^2 = 0.11, SER= 8.7 $$

*** =instructions
The sample average class size across 50 classrooms is 22.8. What is the sample average of the test scores across the 50 classrooms?

*** =hint

Review the formulas for the OLS estimators!

*** =sample_code
```{}
# What is sample average of the test score across the 50 classrooms?


```

*** =solution
```{r}
# First, define:
beta_hat_0 <- 640.3
beta_hat_1 <- -4.93
avg_cs <- 22.8

# Using the OLS formula for beta_hat_0:
avg_ts <- beta_hat_0 + beta_hat_1 * avg_cs
avg_ts
```

*** =sct
```{r}
test_output_contains("527.896", incorrect_msg = "Not correct...")
```

--- type:NormalExercise lang:r xp:50 skills:1 key:39aef8ac4c
## Interpreting OLS Regressions IV

Suppose that a researcher, using data on class size $CS$ and average test scores from 50 third-grade classes, estimates the OLS regression:

$$ \widehat{TestScore} = 640.3 - 4.93 \times CS, R^2 = 0.11, SER= 8.7 $$

*** =instructions
What is the sample standard deviation of test scores across the 50 classrooms?

*** =hint

Review the formulas for the $R^2$ and $SER$ 

$ R^2 = \frac{SSR}{TSS} $

$ SER = \sqrt{\frac{SSR}{n-2}} $

and

$ SSR = \sum_{i=1}^n u^2 $

*** =sample_code
```{r}
# What is sample standard deviation of test scores across the 50 classrooms?


```

*** =solution
```{r}
# Define:
SER <- 8.7
R2 <- 0.11
n <- 50
K <- 2

# Using the formulas:

SSR <- SER^2 * (n-K)
TSS <- SSR/R2 

# Hence, using the forumula for sample standard deviation:

sigma_hat <- sqrt(1/(n-1) * TSS)

# Print it

sigma_hat
```

*** =sct
```{r}
test_output_contains("sigma_hat", incorrect_msg = "Something's wrong... Did you use the forumula for sample standard deviation?")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:2d231a7828
## Inference in the Simple Regression Model

--- type:NormalExercise lang:r xp:100 skills:1 key:c4b2c27865
## Dummy Variables



--- type:NormalExercise lang:r xp:100 skills:1 key:79d4a98b65
## Heteroskedasticity I

In this block of exercises we will use the `cars` data set to explore ways to detect and to deal with heteroskedasticity when estimating simple linear models.

We will discuss two ways of detecting heteroskedasticity:

- Graphical inspection
- Statistical tests

We have already loaded the `AER` package for You.

*** =pre_exercise_code
```{r}
library(AER)
```

*** =instructions
- Get an overview over the data set using `summary()`
- Plot speed (`speed`) against distance (`dist`)
- Estimate the model $dist = \beta_0 + \beta_1 \times speed$. Store the restut in `mod`

*** =sample_code
```{r}
# Get an overview over the data


# Plot speed against distance


# Estimate the model


```

*** =solution
```{r}
# Get an overview over the data
summary(cars)

# Plot speed against distance
plot(cars$speed, cars$dist)

# Estimate the model
mod <- lm(cars$dist ~ cars$speed)

```

*** =sct
```{r}
test_function_result("summary")
test_function("plot", args=c("x","y"))
test_or(
  test_function("lm", eq_condition = "equal"),
  test_function("lm", eq_condition = "equivalent")
)
test_object("mod", eval=F)
success_msg("You are doing great!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:324d782dca
## Heteroskedasticity II

The object `mod` from the previous exercise is available in Your workspace. 


*** =pre_exercise_code
```{r}
library(AER)
plot(cars$speed, cars$dist)
mod <- lm(cars$dist ~ cars$speed)
```

*** =instructions

- Add the regression line for the model `mod` to the plot

By means of simply plotting the data, it is not always easy to decide whether there is heteroskedasticity or not, especially if your data set has more than two variables. Here, it seems that there is more dispersion in `dist` for observations around the mean of `speed`. Let us have a closer look:

- Applying `plot()` to a model model object like `model` produces a whole battery of diagnostic plots. Check this (Your can navigate through the different plots using the buttons).

An indicator for heteroskedasticity is dependence of residuals on the level of fitted values.

- See how fitted values relate to residuals: `plot(mod,1)`

*** =sample_code
```{r}
# Add the regression line for the model mod to the plot
plot(cars$speed, cars$dist)

# Call plot() on your model


# See how fitted values relate to residuals


```

*** =solution
```{r}
# Add the regression line for the model mod to the plot
plot(cars$speed, cars$dist)
abline(mod)

# Call plot() on your model
plot(mod)

# See how fitted values relate to residuals
plot(mod,1)
```

*** =sct
```{r}
test_function("abline")
test_function("plot", index=1)
test_function("plot", index=2)
test_student_typed("plot(mod,1)", not_typed_msg = "Make sure to call the plot as proposed in the instruction.")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:2905f44fda
## Heteroskedasticity III

A formal test for heteroskedasticity was proposed by *Breusch and Pagan (1979)*.<br>
This test checks for heteroskedasticity by fitting a linear model to regression residuals and then tests if regressors are significant in explaining observed variance in the residuals. 

The null hypothesis is no heteroskedasticity.

An R implementation can be found in the package `lmtest`. The function is named `bptest`. By default, regressors from the original regression are used.

*** =pre_exercise_code
```{r}
library(AER)
mod <- lm(cars$dist ~ cars$speed)
```

*** =instructions

The object `mod` from the previous exercise is available in Your R session. 

- Load the `lmtest` package
- Check the help file entry for `bptest`
- Conduct the Breusch-Pagan test


*** =sample_code
```{r}
# Load the `lmtest` package


# Check the help file entry for `bptest`


# Conduct the Breusch-Pagan test
```

*** =solution
```{r}
# Load the `lmtest` package
library(lmtest)

# Check the help file entry for `bptest`
?bptest

# Conduct the Breusch-Pagan test
bptest(mod)
```

*** =sct
```{r}
test_student_typed("library(lmtest)")
test_student_typed("?bptest")
test_function("bptest", args = "formula")
```


--- type:MultipleChoiceExercise lang:r xp: skills: key:2a463d1c54
## Heteroskedasticity IV

Let us have another look on the results of the Breusch-Pagan test.

We have printed the test function's ouput. 

Which statement is correct? (Remember: You may use the console in the panel on the right)


`studentized Breusch-Pagan test`<br>
`data:  mod`<br>
`BP = 3.2149, df = 1, p-value = 0.07297`


*** =instructions

- It is not possible to see wheather the null is rejected without further investigation
- The test does not reject at a level of $\alpha = 0.05$ since $p$-value $>0.05$
- The test does reject at a level of $\alpha = 0.05$ sinse $p$-value $>0.05$
- The test rejects clearly since the test statistic is bigger than the level of significance $\alpha=0.05$

*** =hint
Check your lecture notes!

*** =pre_exercise_code
```{r}
library(AER)
library(lmtest)
mod <- lm(cars$dist ~ cars$speed)
```

*** =sct
```{r}
msg_bad <- "No, that is not correct! You solely have to apply basic knowledge about hypothesis testing... "
msg_success <- "Exactly! The null cannot be rejected. We conclude that there is homoskedasticity. The next exercise will teach you how to visualize this."
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_success, msg_bad, msg_bad))
```

--- type:NormalExercise lang:r xp: skills: key:3734662b44
## Heteroskedasticity V 

We stored the results from the previously conducted Breusch-Pagan test for You. The object's name is `bp`. Use the console to convince yourself that it exisits and what info is stored using the `$` operator.


Put simply, the Breusch-Pagan test is a right-sided test where the test statistic is $\tau \sim \chi_v^2$ with $v = 1$ degrees of freedom. $v$ equals the number of regressors used in the residual regression.


*** =instructions

- Save the test statistic to `tau`. Compute the $p$-value yourself: $p$-value $=1-F(\tau)$ wherby $\tau$ is the observed test statistic and $F$ is the cummulative distribution function of a $\chi_1^2$ random variable.  Hint: Use `pchisq()`
- Build a vector `chi` containing the density of the $\chi_1^2$ distribution at `seq(0,6,0.01)` using `dchisq()`. Save `seq(0,6,0.01)` to `X`
- Draw a simple line plot depicting the density at `seq(0,6,0.01)`. Complete the code suggested in `script.R`.
- Add a point to the plot indicating the density value of the density function at `tau`.

*** =hint

- Use the `$` operator to access the value of the test statistic stored in `bp`
- Remember the help function! See what `pchisq()` and `dchisq()` can do for you.
- Points can be added to an existing plot with `points`. 

*** =pre_exercise_code
```{r}
library(AER)
library(lmtest)
mod <- lm(cars$dist ~ cars$speed)
bp <- bptest(mod)
```

*** =sample_code
```{r}
# Compute the p-value


# Build vectors X and chi


# Draw a line plot depicting the density
plot(    type = "l", col="steelblue", lwd=2)

# Mark the density at tau
```

*** =solution
```{r}
# Create tau and compute the p-value
tau <- bp$statistic
1-pchisq(tau, df=1)

# Build the vectors X and chi
X <- seq(0,6,0.01)
chi <- dchisq(X, df=1)

# Draw a line plot depicting the density of the test statistic
plot(X, chi, type = "l", col="steelblue", lwd=2)

# Mark the density at tau
points(tau,dchisq(tau,1),pch=19, col="red")
```

*** =sct
```{r}
test_object("tau", undefined_msg = "Seems like you did not define `tau`.",
            incorrect_msg = "`tau` does not correspond to the test statistic of the Breusch-Pagan test.")
test_output_contains("1-pchisq(bp$statistic, df=1)")
test_object("X")
test_object("chi")
test_function("plot", args=c("x","y","type"))
test_function("points", args=c("x","y"))
```

--- type:MultipleChoiceExercise lang:r xp:100 skills:1 key:726a6d460b
## The Gauss Markov Theorem I

Suppose you got the regression model

# Not Working

$$ y_i=\beta_0 $$

# Working

$$ \chi^2_{12} $$

In the plotting area on the right you see the result of a Monte Carlo simulation analysing distributional properties of the OLS estimator for $ \beta $ in the model above and another linear estimator $\overset{\sim}{\beta}$ which uses different weights than OLS. Say, $\beta=0$. Is the result consistent with what you expect beeing aware of the Gauss-Markov Theorem?  

*** =instructions
- Yes, both estimators seem to be unbiased but the OLS estimator has less dispersion.
- No, the distribution of $\overset{\sim}{\beta}$ looks more like a standard normal distribution.
- Cannot be answered without prior inspection of data.

*** =pre_exercise_code
```{r}
# Set sample size and number of repititionas

n <- 100      
reps <- 1e5

# Choose epsilon and create a vector of weights as defined above

epsilon <- 0.8
w <- c( rep((1+epsilon)/n,n/2), rep((1-epsilon)/n,n/2) )

# Draw random sample y_1,...,y_N from the standard normal distribution 
# Compute both estimates 1e6 times and store the result in vectors  

ols <- rep(NA,reps)
weightedestimator <- rep(NA,reps)

for (i in 1:reps)
{
  y <- rnorm(n)
  ols[i] <- mean(y)
  weightedestimator[i] <- crossprod(w,y)
}

# Plot estimates of the estimators distribution 

plot(density(ols),col="purple", lwd=3, main="Density of OLS and Weighted Estimator",xlab="")
lines(density(weightedestimator),col="steelblue", lwd=3) 
abline(v=0,lty=2)
legend('topright', c("OLS","weighted"), col=c("purple","steelblue"),lwd=3)
```
*** =sct
```{r}
msg_bad <- "That is not correct!"
msg_success <- "Exactly!"
test_mc(correct = 1, feedback_msgs = c(msg_success, msg_bad, msg_bad))
```