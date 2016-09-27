---
title       : OLS Basics 
description : This section contains exercises dealing with the simple linear regression model and estimation using ordinary least squares. 
attachments :
  slides_link : https://github.com/Emwikts1970/URFITE_DC/raw/master/Econometrics

--- type:NormalExercise lang:r xp:50 skills:1 key:35167f113b
## Multiple Regression: Boston Housing Data

*** =instructions
- Attach the package `MASS`
- Load the Boston housing data set (`Boston`)
- Regress the median housing value in a destrict (`medv`) on the average age of the buildings (`age`) and the crime rate (`crim`) 


*** =hint
Have a look at the plot. What can you say about the dispersion of observations?

*** =sample_code
```{r}
# Attach the package


# Load the data set   


# Conduct the regression

```

*** =solution
```{r}
# Attach the package
library(MASS)

# Load the data set   
#data("Boston")

# Conduct the regression
mod <- lm(medv ~ age + crim,data = Boston)
```


*** =sct
```{r}
test_function("library", args = "package",
              not_called_msg = "You didn't call `library()`!",
              incorrect_msg = "You didn't call `library()` with the correct argument, `package`.")
              
    
test_function("lm", args = "formula",
              not_called_msg = "You didn't call `lm()`!",
              incorrect_msg = "You didn't call `lm()` with the correct argument, `formula`.")

test_object("mod")
```
