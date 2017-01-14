---
title       : Basics in R
description : This section teaches you basic commands in R.

--- type:NormalExercise lang:r xp:150 skills:1 key:3db79c581d
## R as a calculator I

***=instructions

- Use R as a calculator. Calculate $3+4$, $6−8$, $3\times 5$ and $\frac{10}{3}$
- Save the result of $\frac{10}{3}$ to a variable, e.g. `x`, by using the `<-` operator: `x <- 10/3`
- Print the content of this object to the console by typing its name and pressing the <i>enter key</i> 
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

#Define a vector `y` ontaining all even numbers from 12 to 20
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
## Loading Data into R – .csv Files

In R, it is often fairly easy to import data. This exercise will teach you how to import .csv files. "csv" means "comma seperated values".

The data set *cps_ch3.csv* is a sample from the current population survey data base. We have uploaded it so you can use url given in the Script as path.

Notice that it is also possible to read data from Your hard disk (the general case). The path then only needs to be set accordingly i.e. it needs to point to file on your hard disk.

*** =instructions

- Load the data set with the help of the function `read.table()`. Assign the result to the object `my_data`. 
Your code should look something like: read.table("dataset_url"). 

It is important to use quotes here to make sure R interprets the url as as string – a sequence of characters – instead of an object.

*** =hint

See `?read.table` for further help.

*** =sample_code
```{r}
# Read in the data set and assign it to my_data
# URL: http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/cps_ch3.csv

```

*** =solution
```{r}
# Read in the data set and assign it to my_data
my_data <- read.table("http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/cps_ch3.csv")
```

*** =sct
```{r}
test_function("read.table")
test_object("my_data")
success_msg("The cool thing about this is: You can access the data from anywhere. Try it yourself: copy, paste and execute Your call of `read.table()` to the console of the R version You have installed on Your computer!")
```

--- type:NormalExercise lang:r xp: skills: key:8b0e455baf
## Print the Data Set

Great! If you want to print your the contents of the object `my_data`, you simply have to type its name (to the console or in your script) and execute. 

***=pre_exercise_code
```{r}
my_data <- read.table("http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/cps_ch3.csv")
```

***=instructions

- Print the data to the console: `my_data`

*** =hint

Write `my_data` into your script.

*** =sample_code
```{r}
# Print the data to the console

```

***=solution
```{r}
# Print the data to the console
my_data
```

*** =sct
```{r}
test_predefined_objects("my_data")
test_output_contains("my_data")
```

--- type:NormalExercise lang:r xp: skills: key:dfeef3533a
## How to get an Overview

When there are many variables and/or many observations, printing the data set can be really messy. 
A better approach to inspect the data set in such cases is to use the `head` function. 
<br>
By default, `head` prints only the first 6 observations of a data set to the console.

***=pre_exercise_code
```{r}
my_data <- read.table("http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/cps_ch3.csv")
```

***=instructions

- Have a look at the first few observations using `head(my_data)`

*** =hint

See `?head` for further help.

*** =sample_code
```{r}
# Have a look at the first few observations

```

*** =solution
```{r}
# Have a look at the first few observations using head(my_data)
head(my_data)
```

*** =sct
```{r}
test_function("head")
success_msg("Well done!")
```

--- type:NormalExercise lang:r xp: skills: key:710866a669
## Wait ... Something's Not Right

The data set should look something like:

  <table>
      <tr>
        <th>a_sex</th>
        <th>year</th>
        <th>ahe_12</th>
      </tr>
      <tr>
        <td>1</td>
        <td>1992</td>
        <td>1.830.968.857</td>
      </tr>
      <tr>
        <td>1</td>
        <td>1992</td>
        <td>1.636.428.452</td>
      </tr>
  </table>
<br>
Instead we have:

  <table>
      <tr>
        <th>V1</th>
      <tr>
        <td>1;1992;1.830.968.857</td>
      </tr>
      <tr>
        <td>1;1992;1.636.428.452</td>
      </tr>
  </table>
<br>

R did not recognise the first row as the table header and instead interpreted the variables `sex`, `year` and `ahe_12` to be one single variable. As a result, R established a new variable `V1` where each observation consists of the respective three values merged in one string.

*Convince Yourself again: Type and execute* `head(my_data)`.

To circumvent this, You need to tell R that the first row of the table is the header providing variable names and how variables are seperated (here, `;` is used as the seperator. You can think of it as a vertical line seperating variables in a table). 

*** =pre_exercise_code
```{r}
my_data <- read.table("http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/cps_ch3.csv")
```

*** =instructions

- Load the data set again. Set `header=TRUE` to tell R that the first line contains variable names and set `sep=";"` for setting the field seprator to `;`. Overwrite the object `my_data` from the previous exercise with the correct table. 

*** =hint

For further information on functions `read.table` and `head()` use the help function `?` in conjunction with the functions name, e.g. `?head`.

*** =sample_code
```{r}
# Check again that my_data consists of one variable V1
head(my_data)

# Load the data set again, this time using arguments sep and header

```

*** =solution
```{r}
# Check again that my_data consists of one variable V1
head(my_data)

# Load the data set again, this time using arguments sep and header
my_data <- read.table("http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/cps_ch3.csv", header = TRUE, sep =";")
```

*** =sct
```{r}
test_function("head")
test_function("read.table", args=c("header","sep"))
test_object("my_data")
success_msg("Cool!")
```

--- type:NormalExercise lang:r xp: skills: key:7131f0e223
## Yes, That Looks Better!

The data set should now look something like:

  <table>
      <tr>
        <th>a_sex</th>
        <th>year</th>
        <th>ahe_12</th>
      </tr>
      <tr>
        <td>1</td>
        <td>1992</td>
        <td>1.830.968.857</td>
      </tr>
      <tr>
        <td>1</td>
        <td>1992</td>
        <td>1.636.428.452</td>
      </tr>
  </table>
<br>

R did not recognise the first row as the table header and instead interpreted the variables `sex`, `year` and `ahe_12` to be one single variable. As a result, R established a new variable `V1` where each observation consists of the respective three values merged in one string.

*Convince Yourself: Type and execute* `head(my_data)`.

To circumvent this, You need to tell R that the first row of the table is the header providing variable names and how variables are seperated (here, `;` is used as the seperator. You can think of it as a vertical line seperating variables in a table). 

*** =instructions

- Have a look at the first few observations again by executing `head(my_data)` to see the effect of the additional arguments.

*** =hint

For further information on functions `read.table` and `head` use the help function `?` in conjunction with the functions name, e.g. `?head`.

*** =pre_exercise_code
```{r}
my_data <- read.table("http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/cps_ch3.csv")
```

*** =sample_code
```{r}
# Inspect the data sets' first observations again using head

```

*** =solution
```{r}
# Inspect the data sets' header again
head(my_data)
```

*** =sct
```{r}
test_output_contains("head(my_data)")
success_msg("Cool! The next exercise shows You how to read in data from .txt files :-)")
```


--- type:NormalExercise lang:r xp: skills: key:75120820eb
## Load Data From .txt Files Into R

We have prepared another data set containing observations from the 1985 Current Population Survey, this time in a .txt file to be found at

*http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/CPS1985.txt*


*** =instructions

- Load the data set and store it to `cps1985`. Make sure to specify the correct field seperator and to set the first row as the table header.
- Convince Yourself that everything went right by inspecting the first few observations with a call of the function `head()`.

*** =hint
For further information on functions `read.table` and `head()` use the help function `?` in conjunction with the functions name, e.g. `?head`.

*** =sample_code
```{r}
# Read in the data set


# Inspect the result using head()


```

*** =solution
```{r}
# Load the data set from the CPS1985.txt file
cps1985 <- read.table("http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/CPS1985.txt", sep=",", header=TRUE)

# Inspect the result using head()
head(cps1985)

```

*** =sct
```{r}
test_function("read.table")
test_object("cps1985")
test_output_contains("head(cps1985)")
success_msg("This looks right! Keep up the good work!")
```

--- type:NormalExercise lang:r xp: skills: key:711663e93b
## Now Have a Look Again ...

Okay. The data set You imported in the last exercise is available in Your environment.

***pre_exercise_code
```{r}
cps1985 <- read.table("http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/CPS1985.txt", sep=",", header=TRUE)
```

***=instructions

Convince Yourself that everything went right by inspecting the first few observations with a call of the function `head`.

*** =hint
For further information on functions `read.table` and `head()` use the help function `?` in conjunction with the functions name, e.g. `?head`.

*** =sample_code
```{r}
# Inspect the result yet again using head()

```

*** =solution
```{r}
# Inspect the result using head()
head(cps1985)
```

*** =sct
```{r}
test_predefined_object("cps1985")
test_output_contains("head(cps1985)")
success_msg("This looks right! Keep up the good work!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:e5dc4639f7
## How to Load a Package

In the subsequent exercises, You will learn how to use data that comes with R packages. We use the `CPSSWEducation` data set contained in the AER package.

*** =instructions
 Load the AER package using the `library` function by executing `library(AER)`. Add the `CPSSWEducation` data set to the workspace with `data("CPSSWEducation")` 

***=hint

For more info on the functions `library` and `data` use the help function!

*** =sample_code
```{r}
# Load the AER package


# Add the data to workspace


```

*** =solution
```{r}
# Load the AER package add the data to workspace
library(AER)
# Add the data to workspace
data("CPSSWEducation")
```

*** =sct
```{r}

test_function("library")

test_function("data",
              not_called_msg = "You didn't call `data()`!",
              incorrect_msg = "You did call `data()` with the wrong argument")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:8a35320e10
## Summarise Your Data

So far so good. Now, if we are interested in computing some descriptive statistics about a data set at hand, the `summary` function is quite convenient.
Check it out!

***=pre_exercise_code
```{r}
library(AER)
data("CPSSWEducation")
```

*** =instructions

Get an overview over the data stored in `CPSSWEducation` with help of the `summary()` function. Type and execute `summary(CPSSWEducation)`. Notice that `summary` is called on an object. In R, an object's name has to be given without quotation marks.

*** =sample_code
```{r}
# Use the summary function on the CPSSWEducation data set 

```

*** =solution
```{r}
# Use the summary function on the CPSSWEducation data set 
summary(object=CPSSWEducation)
```

*** =sct
```{r}
test_function("summary", args = "object",
              not_called_msg = "You didn't call `summary()`!",
              incorrect_msg = "You did call `summary()` with the wrong argument, `object`!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:ad8022dbb5
## Your First data.frame

`CPSSWEducation` is a `data.frame` object. For now, you can think of it as a matrix where variables are stored in named columns. You can select a specific variable using the `$` operator.

***=pre_exercise_code
```{r}
library(AER)
data("CPSSWEducation")
```

***=instructions

Print observations for `education` using the command `CPSSWEducation$education`. 

*** =sample_code
```{r}
# Print observations of `education`.

```

*** =solution
```{r}
# Print observations of `education`
CPSSWEducation$education
```

***=sct
```{r}
test_student_typed("CPSSWEducation$education", 
                    not_typed_msg = "You failed printing observations of `education`. There must be a typo! Look again at Your Code!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:96ffc27bc6
## Attaching Data Sets

Use the `attach` function, You can add data set to R's search path. You are then able to access variables stored in the dataset by simply naming them.

***=pre_exercise_code
```{r}
library(AER)
data("CPSSWEducation")
```

*** =instructions

Type `attach(CPSSWEducation)`. Then, check if it worked: Execute `education`!

*** =sample_code
```{r}
# Attach the data set to R's search path

```

*** =solution
```{r}
# Attach the data set to R's search path
attach(CPSSWEducation)
```

***=sct
```{r}
test_function("attach", args = "what",
              not_called_msg = "You didn't call `attach()`!",
              incorrect_msg = "You did call `attach()` with the wrong argument, `what`!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:e2c89224e2
## Your First Scatter Plot

Now suppose you are interested in the relation between earnings and education. As a first step, it might be a good idea to create a simple plot to
visualise the relationship. In R, you can do this by means of the `plot` function.

***=pre_exercise_code
```{r}
library(AER)
data("CPSSWEducation")
attach(CPSSWEducation)
```

*** =instructions

Use `plot(education, earnings)` to create a scatter plot of observations on these variables

*** =sample_code
```{r}
# Plot observations on education and earnings

```

*** =solution
```{r}
# Plot observations on education and earnings
plot(education, earnings)
```

*** =sct
```{r}
test_function("plot", args = c("x","y"),
              not_called_msg = "You didn't call `plot()`!",
              incorrect_msg = "You did call `attach()` with the arguments, `x` and `y`!")

test_error()
success_msg("Well done! In the next exercise, You will learn some more data wrangling techniques.")
```

--- type:NormalExercise lang:r xp:100 skills:1  key:89349eccc2
## Data Wrangling with the CPS Data Set

In this exercise, you will learn some more tricks in data wrangling. We already loaded the `cps1985` dataset for you, it is available in the environment of you R session for the next bunch of exercises.
<br>
`cps1985` contains a subset of observations from the <a href="http://www.census.gov/programs-surveys/cps.html">Current Population Survey</a>.   


*** =pre_exercise_code
```{r}
cps1985 <- read.table("http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/CPS1985.txt", sep=",", header=TRUE)
```

*** =instructions
Get an overview over the data set. Check its dimensions using the function `dim` and compute some descriptive statistics with `summary`.

*** =sample_code
```{r}
# Check dimensions and compute descriptive statistics
```

*** =solution
```{r}
# Check dimensions and compute descriptive statistics
dim(cps1985)
summary(cps1985)
```

*** =sct
```{r}
test_function("dim", args="x",
              not_called_msg = "You didn't call `dim()`!",
              incorrect_msg = "You did call `dim()` with the wrong argument")

test_function("summary", args = "object",
              not_called_msg = "You didn't call `summary()`!",
              incorrect_msg = "You did call `summary()` with the wrong argument, `object`!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:ef9f334525
## CPS Data -  Subsetting

Let's see how You can extract a subset of observations for a certain variable... 

***=pre_exercise_code
```{r}
cps1985 <- read.table("http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/CPS1985.txt", sep=",", header=TRUE)
```

***=instructions
Print the first 100 observations of the variable `wage` to the console using operators `[` and `]`. Example: `cps1985$wage[1:10]` prints the first 10 observations for wage.

***=sample_code
```{r}
# Use the [ ] operators to print the first 100 observations of wage

```

***=solution
```{r}
# Use the [ ] operators to print the first 100 observations of `wage` to the console
cps1985[100,1]
```

***=sct
```{r}
test_output_contains("cps1985[100,1]",
                         incorrect_msg = "Have you used `[100, 1]` to print the first 100 obs. from `wage` in `cps1985`?")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:335ebfa520
## If You Don't Care About Union Status...

If You are only interested in some variables of your data set, it might come handy to exclude uninteresting ones.

***=pre_exercise_code
```{r}
cps1985 <- read.table("http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/CPS1985.txt", sep=",", header=TRUE)
```

***=instructions
Store all variables contained in `cps1985` except for `union` in a new object named `cps1985new`.

***=sample_code
```{r}
# Create a new object cps1985new containing all variables from cps1985 except for union


```

***=solution
```{r}
# Create a new object cps1985new containing all variables from cps1985 except for union
cps1985new <- cps1985[,-10]
```

***=sct
```{r}
test_object("cps1985new",
            undefined_msg = "You did not define an object named `cps1985new`!",
            incorrect_msg = "The data set does not look the way it is supposed to be... Maybe You did something wrong with the indexing?")

test_error()
success_msg("Good work!")
```

--- type:NormalExercise lang:r xp:100 skills:1  key:e0d56bf08c
## Create Your Own Matrix

***=instructions

Construct a 3x3 matrix `X` containing numbers from 1 to 9 rowwise using `matrix()`

***=hint

See `?matrix`.

***=sample_code
```{r}
# Construct a 3x3 matrix `X` containing numbers from 1 to 9 rowwise using the matrix function

```

***=solution
```{r}
# Construct a 3x3 matrix `X` containing numbers from 1 to 9 rowwise using the matrix function
X <- matrix(c(1,2,3,4,5,6,7,8,9), nrow=3, byrow=T)
```

***=sct
```{r}
test_object("X",
            undefined_msg = "You did not define an object named `X`!",
            incorrect_msg = "The matrix does not look the way it is supposed to be... Maybe you confused rows with columns?")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:d1339599b1
## Joining Vectors Columnwise

You can also join vectors to Matrices. 

*** =instructions

Create two arbitrary numeric column vectors of length three named `x` and `y` and join them columnwise using `cbind()`. Store the resulting 3x2 matrix in `Y`.

*** =sample_code
```{r}
# Create two vectors x = (1 2 3)'  and y = (4 5 6)' and join them using cbind. Store the result in Y.

```

*** =solution
```{r}
# Create two vectors x = (1 2 3)'  and y = (4 5 6)' and join them using cbind. Store the result in Y.
x <- c(1,2,3)
y <- c(4,5,6)
Y <- cbind(x,y)
```

***=sct
```{r}
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
```

--- type:NormalExercise lang:r xp:100 skills:1 key:9d7d7fe36b
## Matrix Product

This exercise teaches You how to compute a matrix product using R.

The matrices `X` and `Y` from the previous exercises are available in your working environment.

***pre_exercise_code
```{r}
X <- matrix(c(1,2,3,4,5,6,7,8,9), nrow=3, byrow=T)
x <- c(1,2,3)
y <- c(4,5,6)
Y <- cbind(x,y)
```

*** =instructions

Compute the matrix product of `X` and `Y` using the `%*%` operator. Store the resulting 3x2 matrix in `A`.

***=sample_code
```{r}
# Determine the matrix product of X and Y. Store the result in A.

```

*** =solution
```{r}
# Determine the matrix product of X and Y. Store the result in A.
A <- X %*% Y
```

***=sct
```{r}
test_predefined_objects(c("X","Y"))
test_object("A")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:a6094cd18c
## Transposing Matrices

Matrices can be transposed using the `t` function.

The Matrix `A` from the last exercise is available in your working environment.

***=pre_exercise_code
```{r}
X <- matrix(c(1,2,3,4,5,6,7,8,9), nrow=3, byrow=T)
x <- c(1,2,3)
y <- c(4,5,6)
Y <- cbind(x,y)
A <- X %*% Y
```

*** =instructions

Transpose `A` using `t`.

*** =sample_code
```{r}
# Transpose A

```

*** =solution
```{r}
# Transpose A
t(A)
```

*** =sct
```{r}
test_predefined_objects("A")
test_output_contains("t(A)",
                         incorrect_msg = "Have you used `t` to transpose `A`?")
test_error()
success_msg("Nicely Done!")
```
