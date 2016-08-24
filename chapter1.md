---
title       : Basics in R
description : This section teaches you basic commands in R.

--- type:NormalExercise lang:r xp:100 skills:1 key:3db79c581d
## Data Handling I

In this exercise, you will learn how to use data that comes with R packages. We use the `CPSSWEducation` data set contained in the AER package.

*** =instructions
- Load the AER package using the `library()` function by executing `library(AER)`. Add the `CPSSWEducation` data set to the workspace with `data("CPSSWEducation")` 
- Get an overview over the data stored in `CPSSWEducation` with help of the `summary()` function. Type and execute `summary(CPSSWEducation)`. Notice that `summary()` is called on an object. In R, an object's name has to be given without quotation marks.
- `CPSSWEducation` is a `data.frame` object. For now, you can think of it as a matrix where variables are stored in named columns. You can select a specific variable using the `$` operator. Print observations for `education` using the command `CPSSWEducation$education` 
- Use the `attach(CPSSWEducation)` command to attach the data set to R's search path. You are now able to access variables stored in the dataset by simply giving their names. Have a try!
- Suppose you are interested in the relation between earnings and education. Use `plot(education, earnings)` to create a scatter plot of observations on these variables

*** =sample_code
```{r}
# Load the AER package and add data to workspace


# Use the summary() function on the CPSSWEducation data set 


# Print observations of `education`


# Attach the data set to R's search path


# Plot observations on education and earnings


```

*** =solution
```{r}
# Load the AER package and add data to workspace
library(AER)
data("CPSSWEducation")

# Use the summary() function on the CPSSWEducation data set 
summary(object=CPSSWEducation)

# Print observations of `education`
CPSSWEducation$education

# Attach the data set to R's search path
attach(CPSSWEducation)

# Plot observations on education and earnings
plot(education, earnings)

```

*** =sct
```{r}

test_function("library")

test_function("data",
              not_called_msg = "You didn't call `data()`!",
              incorrect_msg = "You did call `data()` with the wrong argument")
              
test_function("summary", args = "object",
              not_called_msg = "You didn't call `summary()`!",
              incorrect_msg = "You did call `summary()` with the wrong argument, `object`!")

test_student_typed("CPSSWEducation$education")

test_function("attach", args = "what",
              not_called_msg = "You didn't call `attach()`!",
              incorrect_msg = "You did call `attach()` with the wrong argument, `what`!")

test_function("plot", args = c("x","y"),
              not_called_msg = "You didn't call `plot()`!",
              incorrect_msg = "You did call `attach()` with the arguments, `x` and `y`!")

test_error()

success_msg("Great! In the next exercise we will learn how to read data from .csv-files")
```
