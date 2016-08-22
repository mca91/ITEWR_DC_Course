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


--- type:NormalExercise lang:r xp:100 skills:1 key:3db79c581d
## The Simple Linear Regression Model I

In this exercise, you will learn how to use R for estimating linear regression models. We use the `CPSSWEducation` data set coming with the AER package.

*** =instructions
- Load the AER package using the `library()` function by executing `library(AER)`. Add the CPSSWEducation data set to the workspace with `data("CPSSWEducation")` 
- Get an overview over the data with help of the `summary()` function. Type and execute `summary(CPSSWEducation)`
- Use the `attach(CPSSWEducation)` command to attach the data set to R's search path. You are now able to access variables stored in the dataset by simply giving their names. Have a try!
- Suppose you are interested in the relation between earnings and education. Use `plot(education, earnings)` to create a scatter plot of observations on these variables

*** =sample_code
```{r}
# Load the AER package and add data to workspace


# Use the summary() function on the CPSSWEducation data set 


# Attach the data set to R's search path


# Plot observations on education and earnings


```

*** =solution
```{r}
# Load the AER package and add data to workspace
library(AER)
data("CPSSWEducation")

# Use the summary() function on the CPSSWEducation data set 
summary(CPSSWEducation)

# Attach the data set to R's search path
attach(CPSSWeducation)

# Plot observations on education and earnings
plot(education, earnings)

```

*** =pre_exercise_code

```{r}
library(AER)
data("CPSSWEducation")
```

*** =sct
```{r}

test_function("library", args = "package",
              not_called_msg = "You didn't call `library()`!",
              incorrect_msg = "You did call `library()` with the wrong argument, `package`!")

test_function("data", args = "list",
              not_called_msg = "You didn't call `data()`!",
              incorrect_msg = "You did call `data()` with the wrong argument, `list`!")
              
test_function("summary", args = "object",
              not_called_msg = "You didn't call `summary()`!",
              incorrect_msg = "You did call `summary()` with the wrong argument, `object`!")

test_function("attach", args = "what",
              not_called_msg = "You didn't call `attach()`!",
              incorrect_msg = "You did call `attach()` with the wrong argument, `what`!")

test_function("plot", args = c("x","y"),
              not_called_msg = "You didn't call `plot()`!",
              incorrect_msg = "You did call `attach()` with the arguments, `x` and `y`!")

test_error()

success_msg("Good work!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:13d4cf0fb6
## Inference in the Simple Regression Model

--- type:NormalExercise lang:r xp:100 skills:1 key:c4b2c27865
## Dummy Variables

--- type:NormalExercise lang:r xp:100 skills:1 key:79d4a98b65
## Heteroskedasticity

--- type:NormalExercise lang:r xp:100 skills:1 key:726a6d460b
## The Gauss Markov Theorem

--- type:NormalExercise lang:r xp:100 skills:1 key:9ad3c5911e
## Introduction to Multiple Regression

