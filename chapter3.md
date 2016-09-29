---
title       : Multiple Regression (test)
description : This section contains exercises dealing with the simple linear regression model and estimation using ordinary least squares. 
attachments :
  slides_link : https://github.com/Emwikts1970/URFITE_DC/raw/master/Econometrics

--- type:NormalExercise lang:r xp:50 skills:1 key:35167f113b
## Multiple Regression: Boston Housing Data

*** =instructions
- Attach the package `MASS`
- Load the Boston housing data set (`Boston`)
- Regress the median housing value in a destrict `medv` on the average age of the buildings `age` and the crime rate `crim`


*** =hint
Have a look at the plot. What can you say about the dispersion of observations?

*** =sample_code
```{r}
# Attach the package


# Load the data set   


# Conduct the regression

```

***=pre_exercise_code
```{r}
library(MASS)
```

*** =solution
```{r}
# Attach the package
library(MASS)

# Load the data set   
data("Boston")

# Conduct the regression
mod <- lm(medv ~ age + crim, data = Boston)
```


*** =sct
```{r}

test_or(
  test_function("lm", eq_condition = "equal"),
  test_function("lm", eq_condition = "equivalent")
)
test_object("mod", eval=F)
```
