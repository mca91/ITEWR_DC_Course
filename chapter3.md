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
test_function("summary", index=1, args="object")


test_or({
  fun <- ex() %>% check_function('lm')
  fun %>% check_arg('formula') %>% check_equal()
  fun %>% check_arg('data') %>% check_equal()
}, {
  ex() %>% override_solution('lm(Boston$medv ~ Boston$lstat)') %>% check_function('lm') %>% check_arg('formula') %>% check_equal()
})

test_or({
    test_function("summary", args="object", index=2)
}, {
    ex() %>% override_solution("summary(lm(Boston$medv ~ Boston$lstat))") %>% check_function('summary') %>% check_arg('object') %>% check_equal()
})
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

test_or({
  ex() %>% check_function('lm') %>% check_result()
}, {
  ex() %>% override_solution('lm(Boston$medv ~ Boston$lstat + Boston$crim + Boston$age)') %>% check_function('lm') %>% check_result()
})

test_or({
    test_function_result("summary")
}, {
    ex() %>% override_solution("summary(lm(Boston$medv ~ Boston$lstat + Boston$crim + Boston$age))") %>% check_function('summary') %>% check_arg('object') %>% check_equal()
})

```



--- type:MultipleChoiceExercise lang:r xp: skills: key:e71f15da13
## Multiple Regression: Boston Housing Data III

The multiple regression model from the previous exercise is available in your environment (`mod`). 

Use the summary function again and have a look at the coefficient section of the output printed to the console.

Do the signs of the coefficient estimates correspond with your expectations? 


*** =instructions

- No: The sign of age is implausible since old houses are decripit such that their value should decrease with their age
- No: The intercept is just around 32.82$ what is far to low for new build houses in districts with zero crime rate and only high-income people
- Probably: We expect a positive intercept ($value \geq 0$). House values should be lower in districts with a high crime rates and a high 
percentage of low income individuals

*** =hint

*** =pre_exercise_code
```{r}
library(MASS)
data("Boston")
mod <- lm(medv ~ lstat + age + crim, data = Boston)
```


*** =sct
```{r}

```
