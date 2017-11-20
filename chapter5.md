---
title       : Heteroskedasticity
description : This chapter teaches you how to detect and how to deal with heteroskedasticity when estimating linear models with R.

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
- Estimate the model $$dist = \beta\_0 + \beta\_1 \times speed + u\_i$$ and store the restut in `mod`

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


--- type:MultipleChoiceExercise lang:r xp: skills: key:8508ba1468
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

--- type:NormalExercise lang:r xp: skills: key:e51917681b
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
