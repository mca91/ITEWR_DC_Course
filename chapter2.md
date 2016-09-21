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
# The pre exercise code runs code to initialize the user's workspace.
# You can use it to load packages, initialize datasets and draw a plot in the viewer
library(sandwich)

set.seed(1)
x <- runif(500, 0, 1)
y <- 5 * rnorm(500, x, x)
plot(y ~ x, col = "steelblue", pch = 19)
```

*** =sct
```{r}
msg_bad <- "That is not correct!"
msg_success <- "Exactly! There seems to be Heteroskedasticity."
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_success, msg_bad, msg_bad))
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
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

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

Suppose that a researcher, using data on class size $CS$ and average test scores from 50 third-grade classes, estimates the OLS regression:

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

a

$x_i$

a

$ SER = \sqrt{ \frac{1}{n-2} \sum_{i=1}^n u_{i}^2 } $


*** =sample_code
```{r}
# What is sample standard deviation of test scores across the 50 classrooms?


```

*** =solution
```{r}
5
```

*** =sct
```{r}
test_output_contains("5")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:2d231a7828
## Inference in the Simple Regression Model

--- type:NormalExercise lang:r xp:100 skills:1 key:c4b2c27865
## Dummy Variables

--- type:NormalExercise lang:r xp:100 skills:1 key:79d4a98b65
## Heteroskedasticity

--- type:NormalExercise lang:r xp:100 skills:1 key:726a6d460b
## The Gauss Markov Theorem

--- type:NormalExercise lang:r xp:100 skills:1 key:9ad3c5911e
## Introduction to Multiple Regression

