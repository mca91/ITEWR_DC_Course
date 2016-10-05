---
title       : Basics in R
description : This section teaches you basic commands in R.

--- type:NormalExercise lang:r xp:100 skills:1 key:3db79c581d
## R as a calculator I

***=instructions

- Use R as a calculator. Calculate 3 + 4, 6 − 8, 3 × 5 and 10 / 3
- Save the result of 10 / 3 to a variable, e.g. `x`, by using the `<-` operator: `x <- 10/3`
- Print the content of this object to the console by typing its name and pressing <i>enter</i>
- Round the result to 2 decimal places using `round(x, 2)`

*** =sample_code
```{r}
# Calculate 3 + 4, 6 − 8, 3 * 5 and 10 / 3


# Save the result of 10 / 3 to some variable


# Print the content of the variable to the console


# Round the result to 2 decimal places


```

*** =solution
```{r}

# Calculate 3 + 4, 6 − 8, 3 * 5 and 10 / 3
3+4
6-8
3*5
10/3

# Save the result of 10 / 3 to some variable
x <- 10/3

# Print the content of the variable to the console
x

# Round the result to 2 decimal places
round(x, 2)

```

*** =sct
```{r}

test_output_contains("3+4", incorrect_msg = "Make sure you solve 3+4")
test_output_contains("6-8", incorrect_msg = "Make sure you solve 6-8")
test_output_contains("3*5", incorrect_msg = "Make sure you solve 3*5")
test_output_contains("10/3", incorrect_msg = "Make sure you solve 10/3")

test_object("x", undefined_msg = "You have not defined an object named `x`",
            incorrect_msg = "Nope, `x` does not contain the result of 10/3")

test_output_contains("x", incorrect_msg = "Did you type `x` to the console?")

test_function("round", args=c("x","digits"))

test_error()
success_msg("Great!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:a15675d543
## R as a calculator II


***=instructions

- Define a vector `x` containing all even numbers from 1 to 10. Hint: Use `seq()`
- Define a vector `y` ontaining all even numbers from 12 to 20
- Calculate $x^y$, $y^x$, $log(x)$, $exp(x)$ and $sqrt(x)$
- Calculate $x+y$, $x-z$, $x*y$ and $x/y$

*** =sample_code
```{r}
# Define a vector x containing all even numbers from 1 to 10


# Define a vector y ontaining all even numbers from 12 to 20


# Calculate x^y, y^x, log(x), exp(x) and sqrt(x)


#Calculate x+y, x-y, x*y and x/y


```

*** =solution
```{r}
# Define a vector x containing all even numbers from 1 to 10
x <- seq(2,10,2)

Define a vector `y` ontaining all even numbers from 12 to 20
y <- seq(12,20,2)

# Calculate x^y, y^x, log(x), exp(x) and sqrt(x)
x^y
y^x
log(x)
exp(x)
sqrt(x)

#Calculate x+y, x-z, x*y and x/y
x+y
x-y
x*y
x/y

```

*** =sct
```{r}


test_object("x", undefined_msg = "You have not defined an object named `x`",
            incorrect_msg = "Nope, `x` is not defined the way it is supposed to be :(")
test_object("y", undefined_msg = "You have not defined an object named `y`",
            incorrect_msg = "Nope, `y` is not defined the way it is supposed to be :(")

test_output_contains("x^y", incorrect_msg = "Make sure you solve x^y")
test_output_contains("y^x", incorrect_msg = "Make sure you solve y^x")
test_output_contains("log(x)", incorrect_msg = "Make sure you solve log(x)")
test_output_contains("exp(x)", incorrect_msg = "Make sure you solve exp(x)")
test_output_contains("sqrt(x)", incorrect_msg = "Make sure you solve sqrt(x)")

test_output_contains("x+y", incorrect_msg = "Make sure you solve x+y")
test_output_contains("x-y", incorrect_msg = "Make sure you solve x-y")
test_output_contains("x*y", incorrect_msg = "Make sure you solve x*y")
test_output_contains("x/y", incorrect_msg = "Make sure you solve x/y")

test_error()
success_msg("Great!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:f8c346e680
## R as a calculator III

*** =instructions
- Vectors `x` and `y` from the previous exercise are available in the environment. Use `c()` to combine both vectors in a new one and store the result in, say `z`.
- Figure out the length of the new vector with `length(z)`.
- Access the $6^{th}$ element of the new Vector by typing `z[6]`
- Sum up the $2^{nd}$, $6^{th}$ and $8^{th}$ element of the new vector. 

*** =pre_exercise_code
```{r}
x <- seq(2,10,2)
y <- seq(12,20,2)
```

*** =sample_code

```{r}
# Use c() to combine both vectors in a new one and store the result in, say z


# Figure out the length of the new vector


# Access the 6th element of the new Vector


# Sum up the 2nd, 6th and 8th element of the new vector


```

*** =solution

```{r}
# Use c() to combine both vectors in a new one and store the result in, say z
z <- c(x,y)

# Figure out the length of the new vector
length(z)

# Access the 6th element of the new Vector
z[6]

# Sum up the 2nd, 6th and 8th element of the new vector
sum(z[c(2,6,8)])

```

*** =sct

```{r}

test_object("z", undefined_msg = "You have not defined an object named `z`",
            incorrect_msg = "Nope, `z` is not defined the way it is supposed to be :(")

test_function("length",
              not_called_msg = "You didn't call `length()`!",
              incorrect_msg = "Something's wrong. Did you `length()` with the right argument?")

test_output_contains("z[6]", incorrect_msg = "You did not access the sixth element of the vector.")

test_output_contains("sum(z[c(2,6,8)])", incorrect_msg = "Something's wrong in your calculation. Give it another try!.")

test_error()
success_msg("Great!")
```

--- type:NormalExercise lang:r xp: skills: key:d42a7e12e7
## Load data from .csv files into R

In R, it is often fairly easy to import data. This exercise will teach you how to import .csv files.

The data set *cps_ch3.csv* is a sample from the current population survey data base. We have uploaded it so you can use the following url as path:

*http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/cps_ch3.csv*

Notice that it is also possible to read data from Your hard disk (the general case). The path then only needs to be set accordingly i.e. it needs to point to file on your hard disk.

*** =instructions

- Load in the data set with the help of the function `read.table()`. Assign the result to the object `cps`. 
Your code should look something like: read.table("dataset_url"). 

It is important to use quotes here to make sure R interprets the url as as string – a sequence of characters – instead of an object.

- Print the data to the console: `my_data`

- Have a look at the first few observations using `head(my_data)`

*** =hint

See `?read.table` for further help.

*** =sample_code
```{r}
# Read in the data set and assign it to my_data


# Print the data to the console


# Have a look at the first few observations


```

*** =solution
```{r}
# Read in the data set and assign it to my_data
my_data <- read.table("http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/cps_ch3.csv")

# Print the data to the console
my_data

# Have a look at the first few observations using head(my_data)
head(my_data)
```

*** =sct
```{r}
test_object("my_data")
test_output_contains("my_data")
test_function("head")
#success_msg("The cool thing about this is: You can access the data from anywhere. Try it yourself: Copy, paste and execute Your call of `read.table()` to the console of the R version You have installed on Your computer!")
```

--- type:NormalExercise lang:r xp: skills: key:711663e93b
## Load data from .txt files into R


*** =instructions

*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}

```

*** =solution
```{r}

```

*** =sct
```{r}

```

--- type:NormalExercise lang:r xp:100 skills:1 key:e5dc4639f7
## Data Handling I

In this exercise, you will learn how to use data that comes with R packages. We use the `CPSSWEducation` data set contained in the AER package.

*** =instructions
- Load the AER package using the `library()` function by executing `library(AER)`. Add the `CPSSWEducation` data set to the workspace with `data("CPSSWEducation")` 
- Get an overview over the data stored in `CPSSWEducation` with help of the `summary()` function. Type and execute `summary(CPSSWEducation)`. Notice that `summary()` is called on an object. In R, an object's name has to be given without quotation marks.
- `CPSSWEducation` is a `data.frame` object. For now, you can think of it as a matrix where variables are stored in named columns. You can select a specific variable using the `$` operator. Print observations for `education` using the command `CPSSWEducation$education` 
- Use the `attach(CPSSWEducation)` command to attach the data set to R's search path. You are now able to access variables stored in the dataset by simply giving their names. Have a try: Execute `education`!
- Now suppose you are interested in the relation between earnings and education. Use `plot(education, earnings)` to create a scatter plot of observations on these variables

*** =sample_code
```{r}
# Load the AER package and add data to workspace


# Use the summary() function on the CPSSWEducation data set 


# Print observations of `education`.


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

test_student_typed("CPSSWEducation$education", 
                    not_typed_msg = "You failed printing observations of `education`. There must be a typo! Look again at your Code!")

test_function("attach", args = "what",
              not_called_msg = "You didn't call `attach()`!",
              incorrect_msg = "You did call `attach()` with the wrong argument, `what`!")

test_function("plot", args = c("x","y"),
              not_called_msg = "You didn't call `plot()`!",
              incorrect_msg = "You did call `attach()` with the arguments, `x` and `y`!")

test_error()
success_msg("Great! In the next exercise, You will learn some basic data wrangling techniques.")
```

--- type:NormalExercise lang:r xp:100 skills:1  key:89349eccc2
## Data Handling II

In this exercise, you will learn some more tricks in data wrangling. We already loaded the `cps1985` dataset for you, it is now available in the environment of you R session.
`cps1985` contains a subset of observations from the <a href="http://www.census.gov/programs-surveys/cps.html">Current Population Survey</a>.   

*** =pre_exercise_code
```{r}
cps1985 <- read.table("http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/CPS1985.txt", sep=",", header=TRUE)
```

*** =instructions
- Get an overview over the data set. Check its dimensions using `dim()` and compute some descriptive statistics with `summary()`
- Print the first 100 observations of `wage` to the console using `[]`
- Store all variables contained in `cps1985` except for `union` in a new object named `cps1985new`

*** =sample_code
```{r}
# Check dimensions and compute descriptive statistics


# Use the [] operators to print the first 100 observations of `wage` to the console


# Create a new object `cps1985new` containing all variables from `cps1985` except for `union`


```

*** =solution
```{r}
# Check dimensions and compute descriptive statistics
dim(cps1985)
summary(cps1985)

# Use the [] operators to print the first 100 observations of `wage` to the console
cps1985[100,1]

# Create a new object `cps1985new` containing all variables from `cps1985` except for `union`
cps1985new <- cps1985[,-1]

```

*** =sct
```{r}
test_function("dim", args="x",
              not_called_msg = "You didn't call `dim()`!",
              incorrect_msg = "You did call `dim()` with the wrong argument")

test_function("summary", args = "object",
              not_called_msg = "You didn't call `summary()`!",
              incorrect_msg = "You did call `summary()` with the wrong argument, `object`!")

test_output_contains("cps1985[100,1]",
                         incorrect_msg = "Have you used `[100, 1]` to print the first 100 obs. from `wage` in `cps1985`?")
                         
test_object("cps1985new",
            undefined_msg = "You did not define an object named `cps1985new`!",
            incorrect_msg = "The data set does not look the way it is supposed to be... Maybe you did somethind wrong with the indexing?")

test_error()
success_msg("Good work!")
```

--- type:NormalExercise lang:r xp:100 skills:1  key:e0d56bf08c
## Data Handling III

This exercise teaches You some tricks using selfgenerated data. 

*** =instructions

- Construct a 3x3 matrix `X` containing numbers from 1 to 9 rowwise using `matrix()`
- Create two arbitrary numeric column vectors of length three named `x` and `y` and join them columnwise using `cbind()`. Store the resulting 3x2 matrix in `Y`
- Compute the matrix product of `X` and `Y` using the `%*%` operator. Store the resulting 3x2 matrix in `A`
- Transpose `A` using `t()`

*** =sample_code
```{r}
# Construct a 3x3 matrix `X` containing numbers from 1 to 9 rowwise using `matrix()`


# Create two vectors `x` = (1 2 3)  and `y` = (4 5 6) and join them using `cbind()`. Store the result in `Y`


# Determine the matrix product of `X` and `Y`. Store the result in `A`


# Transpose `A`


```

*** =solution
```{r}
# Construct a 3x3 matrix `X` containing numbers from 1 to 9 rowwise using `matrix()`
X <- matrix(c(1,2,3,4,5,6,7,8,9), nrow=3, byrow=T)

# Create two vectors `x` = (1 2 3)  and `y` = (4 5 6) and join them using `cbind()`. Store the result in `Y`
x <- c(1,2,3)
y <- c(4,5,6)
Y <- cbind(x,y)

# Determine the matrix product of `X` and `Y`. Store the result in `A`
A <- X %*% Y

# Transpose `A`
t(A)


```

*** =sct
```{r}
test_object("X",
            undefined_msg = "You did not define an object named `X`!",
            incorrect_msg = "The matrix does not look the way it is supposed to be... Maybe you confused rows with columns?")

test_object("x",
            undefined_msg = "You did not define an object named `x`!",
            incorrect_msg = "The vector does not look the way it is supposed to be... Print it to the console and see what's wrong!")


test_object("y",
            undefined_msg = "You did not define an object named `y`!",
            incorrect_msg = "The vector does not look the way it is supposed to be... Print it to the console and see what's wrong!")

test_function("cbind")

test_object("Y",
            undefined_msg = "You did not define an object named `Y`!",
            incorrect_msg = "The matrix does not look the way it is supposed to be...")

test_object("A")

test_output_contains("t(A)",
                         incorrect_msg = "Have you used `t()` to transpose A?")

test_error()
success_msg("Nice!")
```
