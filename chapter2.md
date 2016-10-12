---
title       : OLS Basics 
description : This section contains exercises dealing with the simple linear regression model and estimation using ordinary least squares. 
attachments :
  slides_link : https://github.com/Emwikts1970/URFITE_DC/raw/master/Econometrics

--- type:NormalExercise lang:r xp: skills: key:9d4515394d
## Regression I: Class Size and Test Score

A researcher wants to analyse the relationship between class size and pupils' average test score. Therefore he measures both variables in 10 different classes obtaining the following results:

  <table>
      <tr>
        <td><b>Class Size</b></td>
        <td>23</td>
        <td>19</td>
        <td>30</td>
        <td>22</td>
        <td>23</td>
        <td>29</td>
        <td>35</td>
        <td>36</td>
        <td>33</td>
        <td>25</td>
      </tr>
      <tr>
        <td><b>Test Score</b></td>
        <td>430</td>
        <td>430</td>
        <td>333</td>
        <td>410</td>
        <td>390</td>
        <td>377</td>
        <td>325</td>
        <td>310</td>
        <td>328</td>
        <td>375</td>
      </tr>
    </table>


*** =instructions

- Create vectors, `cs` for class sizes and `ts` for test scores, containing the results
- Draw a scatter plot of the results using `plot`
- Compute mean, median and variance and standard deviation of test scores. Use existing R functions!
- Compute both the covariance and pearson's correlation coefficient for `cs` and `ts` using R functions
- Estimate a linear regression of test score on class size using `lm()`. Store the result in `mod`
- `mod` is an object of type `list` with named entries. Check this using the function `is.list()`
- See what information you can obtain from `mod` using the `$` operator. Read out an arbitrary entry of `mod` 


*** =hint



*** =sample_code
```{r}
# Create both vectors


# Draw the scatter plot


# Compute mean, median, variance & standard deviation of test score


# Compute the covariance and the correlation coefficient


# Estimate the regression model and store it in mod


# Check that mod is an object of type list 


# Read out some arbitrary entry of mod using $


```

*** =solution
```{r}
# Create both vectors
cs <- c(23, 19, 30, 22, 23, 29, 35, 36, 33, 25)
ts <- c(430, 430, 333, 410, 390, 377, 325, 310, 328, 375)

# Draw the scatter plot
plot(cs,ts)

# Compute mean, median, variance & standard deviation of test score
mean(ts)
median(ts)
var(ts)
sd(ts)

# Compute the covariance and the correlation coefficient
cov(cs,ts)
cor(cs,ts)

# Estimate the regression model and store it in mod
mod <- lm(ts ~ cs)

# Check that mod is an object of type list 
is.list(mod)

# Read out some arbitrary entry of mod using. E.g. fitted values:
mod$fitted.values

```

*** =sct
```{r}
test_object("cs")
test_object("ts")

test_function("plot")

test_function("mean")
test_function("median")
test_function("var")
test_function("sd")
test_function("cov")
test_function("cor")

test_or(
  test_function("lm", eq_condition = "equal", not_called_msg = "You didn't call `lm()`!",
              incorrect_msg = "You didn't call `lm()` with the correct argument, `formula`."),
  test_function("lm", eq_condition = "equivalent", not_called_msg = "You didn't call `lm()`!",
              incorrect_msg = "You didn't call `lm()` with the correct argument, `formula`.")
)

test_object("mod")

test_function("is.list", args="x")

test_student_typed("mod$")

```

--- type:NormalExercise lang:r xp: skills: key:6e64f67c78
## Regression II: Class Size and Test Score

Consider again the relation of class size and test score. The model object `mod` from the previous exercise is available in your workspace. This means you can use it for subsequent tasks. Convince yourself by typing `summary(mod)` in to the console and get yet again detailed information on the estimated model!



*** =instructions

- Obtain an overview over the model object `mod` using `summary()`
- Add the regression line to the scatterplot. Hint: use `abline()`
- Store the regression summary into `summary`. Discover what information you can extract from `summary` by use of the `$` operator
- Suppose you are interested in how good the model fits the data. Create a new variable `R2` storing the regression's $R^2$
- You can extract a named $2\times4$ matrix with, amongst other things, estimated coefficients and standard errors. Save this matrix to an object named `coef`

*** =hint

*** =pre_exercise_code
```{r}
cs <- c(23, 19, 30, 22, 23, 29, 35, 36, 33, 25)
ts <- c(430, 430, 333, 410, 390, 377, 325, 310, 328, 375)
mod <- lm(ts ~ cs)
```

*** =sample_code
```{r}
# Use summary() the get an overview over your model


# Add the regression line the the scatterplot
plot(cs,ts)

# Store summary(mod) into summary


# Store the regression's R^2 in R2


# Save the coefficient matrix to coef
```

*** =solution
```{r}
# Use summary() the get an overview over your model
summary(mod)

# Add the regression line the the scatterplot
plot(cs,ts)
abline(mod)

# Store summary(mod) into summary
summary <- summary(mod)

# Store the regression's R^2 in R2
R2 <- summary$r.squared

# Save the coefficient matrix to coef
coef <- summary$coefficients

```

*** =sct
```{r}
test_predefined_objects("mod")
test_function("summary")
test_function("abline")
test_object("summary")
test_object("R2")
test_object("coef")
```

--- type:NormalExercise lang:r xp: skills: key:449f4c19de
## Regression III: Class Size and Test Score 

So far, You have conducted regressions where the model consisted of an intercept and another regressor. In this exercise you will learn ways to specify and to 
estimate regression models without the intercept.

*Vectors `cs` and `ts` as well as the list object `mod` from previous exercises are availabe in your working environment.*


*** =instructions

- Use the help function on `lm` (`?lm`) to find out how to specify a `formula` for a regression of `ts` solely on `cs`, i.e. a regression witouh intercept
- Estimate the regression model without intercept and store it in `mod_ni`
- Convince yourself that everything went right. Extract the coefficient matrix from the models summary and store it to `coef`
- Plot both regression lines

*** =hint

- In `lm()` use `ts ~ cs - 1` as the `formula` argument to estimate a regession model lacking an intercept

*** =pre_exercise_code
```{r}
cs <- c(23, 19, 30, 22, 23, 29, 35, 36, 33, 25)
ts <- c(430, 430, 333, 410, 390, 377, 325, 310, 328, 375)
mod <- lm(ts ~ cs)
```

*** =sample_code
```{r}
# Regress ts solely and cs, sore it to mod_ni


# Extract the coefficient matrix from the models summary, save it to coef


# Plot regression lines for both models
plot(cs,ts)

```

*** =solution
```{r}
# Regress ts solely and cs, sore it to mod_ni
mod_ni <- lm(ts ~ cs - 1) # or: lm(ts ~ cs + 0)

# Extract the coefficient matrix from the models summary, save it to coef
coef <- summary(mod_ni)$coefficients

# Plot regression lines for both models
plot(cs,ts)
abline(mod)
abline(mod_ni)

```

*** =sct
```{r}
test_predefined_objects("mod")

test_correct(test_function("lm"),
    {
    test_student_typed("ts ~ cs + 0")
    }
)

test_function("lm")

test_object("mod_ni", eval=F)
test_object("coef")

test_function("abline", index=1)
test_function("abline", index=2)
```

--- type:NormalExercise lang:r xp: skills: key:673ab4d8fc
## Regression IV: Class Size and Test Score  

We now go back to the simple model including an intercept. The estimated regression line for `mod` was

$$ \widehat{TestScore} = 567.43 - 7.15 \times ClassSize, \, R^2 = 0.8976, \, SER=15.19 $$

*You can check this as `mod` and vectores `cs` and `ts` are available in your working environment again.*

*** =instructions
- Compute $SSR$, the sum of squared residuals, and save it to `ssr`
- Compute $TSS$, the total sum of squares, and save it to `tss`
- Use `ssr` and `tss` to compute $R^2$, the coefficient of determination. Save it to R2
- Use the logical expression `==` to check whether your result for $R^2$ equals the one mentioned above

*** =hint

The solutions can be found in several ways, e.g. using formulas and/or knowledge about the structure of `lm` objects. Don't forget about the `$` operator!

*** =pre_exercise_code
```{r}
cs <- c(23, 19, 30, 22, 23, 29, 35, 36, 33, 25)
ts <- c(430, 430, 333, 410, 390, 377, 325, 310, 328, 375)
mod <- lm(ts ~ cs)
```

*** =sample_code
```{r}
# Compute the SSR and save it to ssr


# Compute the TSS and save it to tss


# Compute R^2 and save it to R2


# Check whether your result is correct


```

*** =solution
```{r}
# Compute the SSR and save it to ssr
ssr <- sum(mod$residuals^2)

# Compute the TSS and save it to tss
tss <- 9*var(ts) # var() computes the unbiased sample variance! => Correct by multiplying with n-1 = 9

# Compute R^2, round it by 4 decimal places and save it to R2
R2 <- round(1-ssr/tss,4)

# Check whether your result is correct
R2 == 0.8976
```

*** =sct
```{r}
test_object("ssr")
test_object("tss")
test_object("R2")

test_predefined_objects("mod")

test_function("round", args="digits", eq_condition="equal")

test_student_typed("R2 == 0.8976", not_typed_msg = "Something is wrong. Make sure You type `R2 ==` followed by the value for R^2 mentioned above.")

test_output_contains("R2 == 0.8976")
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:13d4cf0fb6
## Interpreting OLS Regressions I

Suppose that a researcher, using data on class size ($CS$) and average test score ($TestScore$) from 50 third-grade classes, estimates the OLS regression:

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

$ SER = \sqrt{\frac{SSR}{n-2}} $

and

$ SSR = \sum_{i=1}^n u^2 $

*** =sample_code
```{r}
# What is sample standard deviation of test scores across the 50 classrooms?


```

*** =solution
```{r}
# Define:
SER <- 8.7
R2 <- 0.11
n <- 50
K <- 2

# Using the formulas:

SSR <- SER^2 * (n-K)
TSS <- SSR/R2 

# Hence, using the forumula for sample standard deviation:

sigma_hat <- sqrt(1/(n-1) * TSS)

# Print it

sigma_hat
```

*** =sct
```{r}
test_output_contains("sigma_hat", incorrect_msg = "Something's wrong... Did you use the forumula for sample standard deviation?")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:c4b2c27865
## Regression when X is a Dummy Variable

Instead of using a continuous regressor $X$, we might be interested in running a regression where the regressor $D_i$ is binary variable or so-called dummy variable. 

For example, we define $X_i$ in the following way:






--- type:NormalExercise lang:r xp:100 skills:1 key:2d231a7828
## Inference in the Simple Regression Model

