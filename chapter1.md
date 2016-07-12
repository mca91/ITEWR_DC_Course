---
title       : OLS Basics 
description : This section contains exercises dealing with the simple linear regression model and estimation using ordinary least squares. 
attachments :
  slides_link : https://s3.amazonaws.com/assets.datacamp.com/course/teach/slides_example.pdf

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:35167f113b
## A really nice exercise about violation of OLS assumptions

Have a look at the plot that showed up in the viewer to the right. Which of the OLS assumptions could be possibly violated?

*** =instructions
- No perfect multicollinearity
- Homoskedasticity
- Outlier are seldom
- Y is $\chi^2_{10}$ distributed

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
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

msg_bad <- "That is not correct!"
msg_success <- "Exactly! There seems to be Heteroskedasticity."
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_success, msg_bad, msg_bad))
```

--- type:NormalExercise lang:r xp:100 skills:1 key:d71e82b5ef
## Regression and Robust Standard Errors

In the previous exercise, you saw example data exhibiting heteroskedasticity. In this exercise, we'll have a look at how 
we can get a regression summary reporting robust standard errors

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
# A data.frame `data` is available in your workspace


# Regress y on x.


# Report coefficients and robust standard errors.


# Add the regression line to the plot.

```

*** =solution
```{r}
# A data.frame `data` is available in your workspace


# Regress y on x. Store the model in `mod`.
mod <- lm(y~x)

# Report coefficients and robust standard errors.
coeftest(mod, vcov.=vcovHC(mod, type="HC0"))

# Plot data and add the regression line to the plot.
plot(x,y)
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
test_function("plot", args = c("x","y"))
test_function("abline")


test_error()

success_msg("Good work!")
```
