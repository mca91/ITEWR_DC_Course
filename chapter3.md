---
title       : Multiple Regression (test)
description : This section contains exercises dealing with the multiple linear regression model and discusses estimation using ordinary least squares. 
attachments :
  slides_link : https://github.com/Emwikts1970/URFITE_DC/raw/master/Econometrics

--- type:NormalExercise lang:r xp: skills: key:af07cdc945
## Multiple Regression: Boston Housing Data

For the course of this section, we will use the `Boston` data set which contains 506 observations concerning housing values in suburbs of Boston. The data set comes with the package `MASS`.

*** =instructions

- Load the package and the data set
- Get youself an overview over the data set using the `summary` function. Hint: Use `?Boston` for detailed info on variables
- Estimate a simple linear regression model explaining *median house value*, `medv`. by the *percent of household with low socioecononomic status*, `lstat`, and a constant. 
- Inspect the model's summary

*** =hint

You only need basic functions here: `library()`, `data()`, `lm()` and `summary`.

*** =pre_exercise_code
```{r}
library(MASS)
```

*** =sample_code
```{r}
# Load the package and the data set


# Get yourself an overview over the data set


# Estimte the model


# Call summary on Your model


```

*** =solution
```{r}
# Load the package and the data set
library(MASS)
data("Boston")

# Get yourself an overview over the data set
summary(Boston)

# Estimate the model
lm(medv ~ lstat, data = Boston)

# Call summary on Your model
summary(lm(medv ~ lstat, data = Boston))
```

*** =sct
```{r}
test_function("library")
test_function("data")
test_function("summary")

test_correct(test_function_result("lm"),
    {
    test_or(
        test_student_typed("Boston$medv"),
        test_student_typed("Boston$lstat")
        )
    }
)

test_function("summary", args="object")
```


--- type:NormalExercise lang:r xp:50 skills:1 key:35167f113b
## Multiple Regression: Boston Housing Data II

Now, let us expand the idea from the previous exercise by adding additional regressors to the model and estimate it again.

*** =instructions

- Regress the median housing value in a destrict, `medv`, on the average age of the buildings, `age`, the per capita crime rate, `crim`, the percentage of individuals with low socioeconomic status, `lstat`, and a constant. 
- Inspect the model summary

*** =hint
You only need basic functions here: `library()`, `data()`, `lm()` and `summary`.
Use the help function to see how to specify additional regressors in the `formula` argument of `lm()`.

*** =sample_code
```{r}
# Conduct the regression


# Inspect the model summary


```

***=pre_exercise_code
```{r}
library(MASS)
```

*** =solution
```{r}
# Conduct the regression
mod <- lm(medv ~ lstat + age + crim, data = Boston)

# Inspect the model summary
summary(mod)


```


*** =sct
```{r}

test_correct(test_function("lm", args=c("formula","data")),
    {
    test_function("attach")
    test_function("lm", args=c("formula"), eq_condition = "equivalent")
    }
)
test_function("summary")
```


