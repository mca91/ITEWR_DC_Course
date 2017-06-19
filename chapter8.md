---
title       : Empirical Exercises - Economic Growth
description : This section deals with the issue of finding determinants to economic growth. We consider data used by Levine et al. in their paper 'Finance and the Sources of Growth', <i> Journal of Financial Econometrics </i>, 2000, 58:261-300


--- type:NormalExercise lang:r xp:100 skills:1 key:498a3c9d06
## Economic Growth I

The following exercises are considered with the subject of economical growth. Basis for this is a real data set containing growth rates from 1960 through 1995 for 65 countries and various other variables that are possible determinants of growth. 

In particular, we are interested in the relationship between growth and trade. A detailed description of the dataset can be found <a href="http://wps.pearsoned.co.uk/wps/media/objects/12401/12699039/empirical/empex_tb/Growth_Description.pdf">here</a>. 

The dataset `ecgrowth` is available in Your workspace.

*** =instructions

- Create a scatterplot of average annual growth (`growth`) on the average trade share (`tradeshare`).

*** =hint

Use the `plot` function.

*** =pre_exercise_code
```{r}
library(foreign)
ecgrowth <- read.dta('http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/Growth.dta')
```

*** =sample_code
```{r}
# plot the data
```

*** =solution
```{r}
#plot the data
plot(ecgrowth$tradeshare, ecgrowth$growth)
```

*** =sct
```{r}
test_function("plot", args = c("x","y"),
              not_called_msg = "You didn't call `plot()`!",
              incorrect_msg = "You did call `plot()` with wrong arguments, `x` and `y`!")

test_error()
success_msg("Well done!")
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:d00801ce93
## Economic Growth II

We are interested in the relationship between growth and trade. A detailed description of the dataset can be found <a href="http://wps.pearsoned.co.uk/wps/media/objects/12401/12699039/empirical/empex_tb/Growth_Description.pdf">here</a>. 

The dataset 'ecgrowth' is available in Your workspace.

Have a closer look at the scatterplot. Does there appear to be any relationship between the variables?


*** =instructions
- Yes, there seems to be positive correlation between `tradeshare` and `growth`
- No, one cannot see any relationship.
- I need to run a regression to answer this question.

*** =hint
Does one variable increase (decrease) if the other increases (decreases)?

*** =pre_exercise_code
```{r}
library(foreign)
ecgrowth <- read.dta('http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/Growth.dta')
plot(ecgrowth$tradeshare, ecgrowth$growth)
```

*** =sct
```{r}
msg_bad <- "That is not correct!"
msg_success <- "Exactly! There seems to be some positive relationship."
test_mc(correct = 1, feedback_msgs = c(msg_success, msg_bad, msg_bad))
```




--- type:NormalExercise lang:r xp:100 skills:1 key:54d05324f1
## Economic Growth III

We are interested in the relationship between growth and trade. A detailed description of the dataset can be found <a href="http://wps.pearsoned.co.uk/wps/media/objects/12401/12699039/empirical/empex_tb/Growth_Description.pdf">here</a>. 

The dataset `ecgrowth` is available in Your workspace.

Have a closer look at the scatterplot, again. There seems to be an outlier.

*** =instructions
- Can you identify the country associated with the observation in the scatterplot? Store its name in `outlier`.
- Remove the outlier from the dataset `ecgrowth`. Name the new dataset as `ecgrowth_new`.

*** =hint

*** =pre_exercise_code
```{r}
library(foreign)
ecgrowth <- read.dta('http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/Growth.dta')
plot(ecgrowth$tradeshare, ecgrowth$growth)
```

*** =sample_code
```{r}
# Identify the outlier. Assign the country's name to an object named outlier.
outlier <-

# Remove the outlier from the dataset.

```

*** =solution
```{r}
# Identify the outlier. Assign the country's name to an object named outlier
id <- which.max(ecgrowth$tradeshare)
outlier <- ecgrowth$country_name[id]

# Remove the outlier from the dataset
ecgrowth_new <- ecgrowth[-id,]
```

*** =sct
```{r}
test_predefined_objects("ecgrowth")
test_object("outlier")
test_object("ecgrowth_new")
```



--- type:NormalExercise lang:r xp:100 skills:1 key:c2facac387
## Economic Growth IV

We are interested in the relationship between growth and trade. A detailed description of the dataset can be found <a href="http://wps.pearsoned.co.uk/wps/media/objects/12401/12699039/empirical/empex_tb/Growth_Description.pdf">here</a>. 

Now assume that economic growth is determined as follows:

$$ Growth = \beta\_0 + \beta\_1 \times TradeShare + \epsilon$$

The datasets `ecgrowth` and `ecgrowth_new` are available in Your workspace.


*** =instructions

- For convinience, attach `ecgrowth`. Run a simple linear regression of `growth` on `tradeshare` using `lm()`. Store the result in `growth_reg`. Try to interpret Your findings.
- Use `growth_reg` with `predict()` to predict the growth rate for a country with a trade share of 0.5

*** =hint

You have to specify the argument `newdata`. This must be a `data.frame` object where each row is an observation of regressors you want to make a prediction for. Note that the column names must equal the regressor names. Here, we have a single regressor `tradeshare`. 

*** =pre_exercise_code
```{r}
library(foreign)
ecgrowth <- read.dta('http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/Growth.dta')
ecgrowth_new <- ecgrowth[-65,]
plot(ecgrowth$tradeshare, ecgrowth$growth)
```

*** =sample_code
```{r}
# Attach the dataset

# Run the regression

# Do the prediction

```

*** =solution
```{r}
# Attach the dataset

attach(ecgrowth)

# Run the regression

growth_reg <- lm(growth ~ tradeshare)

# Do the prediction

predict(growth_reg, newdata = data.frame(tradeshare = 0.5))
```

*** =sct
```{r}
test_function("attach")
test_object("growth_reg")
test_function("predict", args = "newdata")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:013431ea1b
## Economic Growth V

We are interested in the relationship between growth and trade. A detailed description of the dataset can be found <a href="http://wps.pearsoned.co.uk/wps/media/objects/12401/12699039/empirical/empex_tb/Growth_Description.pdf">here</a>. 

The datasets `ecgrowth` and `ecgrowth_new` are available in Your workspace.

The estimated regression equation from the last exercise is

$$ Growth = 0.6403 + 2.3064 \times TradeShare. $$ 

We continue with another regression.

*** =instructions

- Re-run the regression from the last exercise but this time without the outlier i.e. exclude Malta. Try to interpret your results
- Use Your results to predict the average growth of a country with a trade share of 0.5

*** =hint

You have to specify the argument `newdata`. This must be a `data.frame` object where each row is an observation of regressors you want to make a prediction for. Note that the column names must equal the regressor names. Here, we have a single regressor `tradeshare`. 

*** =pre_exercise_code
```{r}
library(foreign)
ecgrowth <- read.dta('http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/Growth.dta')
ecgrowth_new <- ecgrowth[-65,]
plot(ecgrowth$tradeshare, ecgrowth$growth)
```

*** =sample_code
```{r}
# Re-run the regression
attach(ecgrowth_new)
growth_new_reg <-

# Do the prediction

```

*** =solution
```{r}
# Re-run the regression
attach(ecgrowth_new)
growth_new_reg <- lm(growth ~ tradeshare)

# Do the prediction
predict(growth_new_reg, newdata = data.frame(tradeshare = 0.5))
```

*** =sct
```{r}
test_function("attach")
test_object("growth_new_reg")
test_function("predict", args = "newdata")
success_msg("Good! Re-running the estimation tells us that the model based on the full dataset predicts higher values for `growth` for larger values of `tradeshare` than the model excluding Malta does.")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:68788ae1d3
## Economic Growth VI

We are interested in the relationship between growth and trade. A detailed description of the dataset can be found <a href="http://wps.pearsoned.co.uk/wps/media/objects/12401/12699039/empirical/empex_tb/Growth_Description.pdf">here</a>. 

Model objects `growth_reg` and `growth_new_reg` are available in Your workspace.

Reconsider the previously conducted regressions. Estimated equations are:

<b> Full dataset </b>

$$ Growth = 0.6403 + 2.3064 \times TradeShare $$ 

<b> Excluding the country Malta </b>

$$ Growth = 0.9574 + 1.6809 \times TradeShare $$

*** =instructions

- Add both regression lines to the scatterplot

*** =hint

*** =pre_exercise_code
```{r}
library(foreign)
ecgrowth <- read.dta('http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/Growth.dta')
ecgrowth_new <- ecgrowth[-65,]
plot(ecgrowth$tradeshare, ecgrowth$growth)
points(ecgrowth$tradeshare[65], ecgrowth$growth[65], col="red", pch=19)
text(ecgrowth$tradeshare[65], ecgrowth$growth[65]-0.5, "Malta")

attach(ecgrowth)
growth_reg <- lm(growth ~ tradeshare)
detach(ecgrowth)

attach(ecgrowth_new)
growth_new_reg <- lm(growth ~ tradeshare)
detach(ecgrowth_new)
```

*** =sample_code
```{r}
# These lines must not be altered. The generate the plot You see on the right
plot(ecgrowth$tradeshare, ecgrowth$growth)
points(ecgrowth$tradeshare[65], ecgrowth$growth[65], col="red", pch=19)
text(ecgrowth$tradeshare[65], ecgrowth$growth[65]-0.5, "Malta")

# Add the regression lines to the plot
```

*** =solution
```{r}
# Add the regression lines to the plot
plot(ecgrowth$tradeshare, ecgrowth$growth)
points(ecgrowth$tradeshare[65], ecgrowth$growth[65], col="red", pch=19)
text(ecgrowth$tradeshare[65], ecgrowth$growth[65]-0.5, "Malta")
abline(growth_reg, col="blue")
abline(growth_new_reg, col="green")
```

*** =sct
```{r}
test_function("abline", index = 1, args = "col")
test_function("abline", index = 2, args = "col")
```




--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:3370d4087a
## Economic Growth VII

Have a look at the estimated regression functions. Why is the regression function that was estimated using the dataset including Malta steeper than the regression function that excludes Malta?

Reconsider the previously conducted regressions. Estimated equations are:

<b> Full dataset </b>

<font color="blue"> $$ Growth = 0.6403 + 2.3064 \times TradeShare $$ </font> 

<b> Excluding the country Malta </b>

<font color="green"> $$ Growth = 0.9574 + 1.6809 \times TradeShare $$ </font> 

*** =instructions

- This is solely due to random errors which cannot be observed
- OLS is sensitive to outliers. Therefore, inclusion of Malta in the dataset causes the estimate of the coefficient of `TradeShare` to be larger than when Malta is excluded
- This cannot be answered without further information

*** =hint

*** =pre_exercise_code
```{r}
library(foreign)
ecgrowth <- read.dta('http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/Growth.dta')
ecgrowth_new <- ecgrowth[-65,]
plot(ecgrowth$tradeshare, ecgrowth$growth)
points(ecgrowth$tradeshare[65], ecgrowth$growth[65], col="red", pch=19)
text(ecgrowth$tradeshare[65], ecgrowth$growth[65]-0.5, "Malta")

attach(ecgrowth)
growth_reg <- lm(growth ~ tradeshare)
detach(ecgrowth)

attach(ecgrowth_new)
growth_new_reg <- lm(growth ~ tradeshare)
detach(ecgrowth_new)

abline(growth_reg, col="blue")
abline(growth_new_reg, col="green")
```

*** =sct
```{r}
msg_bad <- "That is not correct!"
msg_success <- "Exactly! Inclusion of an outlier may considerably distort OLS parameter estimates. This means we should exclude such an observation."
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_success, msg_bad))
```

--- type:NormalExercise lang:r xp:100 skills:1 key:8515865794
## Economic Growth VIII

In light of the last couple of exercises, we continue our analysis using the dataset `ecgrowth_new` which exlcudes Malta.

The regression model `growth_new_reg` is available in Your workspace. 
<br>
<br>
Can you reject the hypothesis $H\_0: \beta\_1 = 0$ vs. a two-sided alternative at the $95\%$ level?

*** =instructions

- Check whether $\beta\_1$ is significantly different from zero using `summary()`
- Assign the corresponding p-value to the variable `pval`
- Compute $95\%$ confidence intervalls for $\beta\_0$ and $\beta\_1$ using `confint()`

*** =hint

*** =pre_exercise_code
```{r}
library(foreign)
ecgrowth <- read.dta('http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/Growth.dta')
ecgrowth_new <- ecgrowth[-65,]
attach(ecgrowth_new)
growth_new_reg <- lm(growth ~ tradeshare)
detach(ecgrowth_new)
```

*** =sample_code
```{r}
# Access statistical information about the model


# Assign the p-value to pval


# Compute the confidence intervalls


```

*** =solution
```{r}
# Access statistical information about the model
summary(growth_new_reg)
# Assign the p-value to pval
pval <- summary(growth_new_reg)$coef[2,4]
# Compute the confidence intervalls
confint(growth_new_reg)
```

*** =sct
```{r}
test_function("summary", args = "object")
test_object("pval")
test_function("confint", args = "object")
```





--- type:NormalExercise lang:r xp:100 skills:1 key:5bb281f125
## Economic Growth IX

Reconsider our regression approach:

$$ Growth = \beta\_0 + \beta\_1 \times TradeShare + \epsilon $$

It is not realstic that a country's trade share is the only factor driving its economic growth. It might be prefarable to employ a model with more regressors. In particular, we could consider the following additional variables:

- `YearsSchool`
- `Oil`
- `Rev_Coups`
- `Assassinations`
- `RGDP60`

Check the <a href="http://wps.pearsoned.co.uk/wps/media/objects/12401/12699039/empirical/empex_tb/Growth_Description.pdf">description</a> for detailed info on variables. 

The dataset `ecgrowth_new` is available in Your workspace. 


*** =instructions

- Start by computing descriptive statistics for all columns of `ecgrowth_new` except `country`. Do so by subsetting the dataset accordingly and using relevant *implemented* R functions. Vectorize Your results. <b>Hint</b>: Use `apply()` on the columns of Your subsetted dataset. See `?apply`.   

*** =hint

- Column means of an array `a` can be computed by using `apply(a, 2, mean)`. `2` is the dimension of the array the function `mean` will be applied over
- Further useful functions are `min()`, `max()` and `sd()`


*** =pre_exercise_code
```{r}
library(foreign)
ecgrowth <- read.dta('http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/Growth.dta')
ecgrowth_new <- ecgrowth[-65,]
```

*** =sample_code
```{r}
# Compute descriptive statistics
min <-
max <-
mean <-
sd <-
```

*** =solution
```{r}
# Compute descriptive statistics
min <- apply(ecgrowth_new[,-1], 2, min)
max <- apply(ecgrowth_new[,-1], 2, max)
mean <- apply(ecgrowth_new[,-1], 2, mean)
sd <- apply(ecgrowth_new[,-1], 2, sd)
```

*** =sct
```{r}
test_object("min", eq_condition = "equal")
test_object("max", eq_condition = "equal")
test_object("mean", eq_condition = "equal")
test_object("sd", eq_condition = "equal")
```



--- type:NormalExercise lang:r xp:100 skills:1 key:ac6a704316
## Economic Growth X

We will now consider the following multiple regression model:

$$ Growth = \beta\_0 + \beta\_1 \times TradeShare + \beta\_2 \times YearsSchool + \beta\_3 \times RevCoups \\\\ + \beta\_4 \times RGDP60 + \beta\_5 \times assasinations + \epsilon $$

*** =instructions

- Estimate the model using OLS. Store the result in `mult_mod`
- What is the value of the coefficient on $RevCoups$, a measure for political and social unrest? Try to interpret the coefficient. You will be asked about it in the next exercise 

*** =hint



*** =pre_exercise_code
```{r}
library(foreign)
ecgrowth <- read.dta('http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/Growth.dta')
ecgrowth_new <- ecgrowth[-65,]
```

*** =sample_code
```{r}
# Estimate the multiple regression model


```

*** =solution
```{r}
# Estimate the multiple regression model
mult_mod <- lm(growth ~., data = ecgrowth_new[,-c(1,3)])
summary(mult_mod)$coef
```

*** =sct
```{r}
test_predefined_objects("ecgrowth_new")
test_object("mult_mod", eval = F)

test_or(
    test_function("lm", args = c("formula", "data")),
    {
    ex() %>% override_solution("attach(ecgrowth_new);lm(growth ~ tradeshare + yearsschool + rev_coups + rgdp60 + assasinations)") %>% check_function("attach")
    ex() %>% override_solution("attach(ecgrowth_new);lm(growth ~ tradeshare + yearsschool + rev_coups + rgdp60 + assasinations)") %>% check_function("lm") %>% check_arg("formula") %>% check_equal()
    }
)
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:1e51b5f0fe
## Economic Growth XI

The estimated regression equation for our extented model is

$$ Growth = 0.6269 -0.0005 \times TradeShare + 1.3408 \times YearsSchool -2.1504 \times RevCoups \\\\ -0.0005 \times RGDP60 + 0.3226 \times assasinations $$ 

How do You interpret the coefficient on $RevCoups$?

The model object `mult_mod` is available in Your workspace. 

*** =instructions

- If a country experiences *any* political insurrections, or similar, we expect economic growth to be *lowered* by $2.1504\%$, on average.
- A *one unit* increase (decrease) in numbers of political unrests is expected to decrease (increase) economic growth by $2.1504\%$.
- If a country experiences *at least one*  political insurrections, we expect economic growth to be *increased* by $2.1504\%$, on average.
- This coefficient on its own right cannot be interpreted directly. 

*** =hint

TBD

*** =pre_exercise_code
```{r}
library(foreign)
ecgrowth <- read.dta('http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/Growth.dta')
ecgrowth_new <- ecgrowth[-65,]
mult_mod <- lm(growth ~., data = ecgrowth_new[,-c(1,3)])
```

*** =sct
```{r}
msg_bad <- "That is not correct!"
msg_success <- "Exactly!"
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_success, msg_bad, msg_bad))
```
--- type:NormalExercise lang:r xp:100 skills:1 key:abc4d7eb94
## Economic Growth XII

<div style="border: #3aaaca 3px solid">

The estimated regression equation for our extented model is

$$ Growth = 0.6269 -0.0005 \times TradeShare + 1.3408 \times YearsSchool -2.1504 \times RevCoups \\\\ -0.0005 \times RGDP60 + 0.3226 \times assasinations $$ 

</div>
<br>
Now remember the descriptive statistics you computed before. Joining them coloumn-wise we get the following table:

<table style="text-align:center"><tr><td colspan="5" style="border-bottom: 1px solid black"></td></tr><tr><td style="text-align:left"></td><td>min</td><td>max</td><td>mean</td><td>sd</td></tr>
<tr></tr><tr><td style="text-align:left">growth</td><td>-2.812</td><td>7.157</td><td>1.869</td><td>1.816</td></tr>
<tr><td style="text-align:left">oil</td><td>0</td><td>0</td><td>0</td><td>0</td></tr>
<tr><td style="text-align:left">rgdp60</td><td>367.000</td><td>9,895.004</td><td>3,130.813</td><td>2,522.979</td></tr>
<tr><td style="text-align:left">tradeshare</td><td>0.141</td><td>1.128</td><td>0.542</td><td>0.228</td></tr>
<tr><td style="text-align:left">yearsschool</td><td>0.200</td><td>10.070</td><td>3.959</td><td>2.553</td></tr>
<tr><td style="text-align:left">rev_coups</td><td>0</td><td>0.970</td><td>0.170</td><td>0.225</td></tr>
<tr><td style="text-align:left">assasinations</td><td>0</td><td>2.467</td><td>0.282</td><td>0.494</td></tr>
<tr><td colspan="5" style="border-bottom: 1px solid black"></td></tr></table>
<br>

The model object `mult_mod` is available in Your workspace.

*** =instructions

- Join all descriptive statistics as shown above in an object of class `data.frame`. Assign the result to `descriptives`.
- Use the function `predict()` to predict the average anual growth rate for an *average* country, i.e. for an observation that has average values for all regressors.

*** =hint

- To join vectors `a`,`b` and `c` to a `data.frame` with named columns, execute `data.frame(a=a, b=b, c=c)`. See also `?data.frame`.
- In Your call of `predict()` You have to specify the argument `newdata`. This must be a `data.frame` object where each row is an observation of regressors you want to make a prediction for. Note that the column names must equal the regressor names. We have five regressors: `tradeshare`, `rgdp60`, `yearsschool`, `rev_coups` and `assasinations`. 
- The function `subset.data.frame()` may be helpful in specifying the argument `newdata` in `predict`.

*** =pre_exercise_code
```{r}
library(foreign)
ecgrowth <- read.dta('http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/Growth.dta')
ecgrowth_new <- ecgrowth[-65,]
min <- apply(ecgrowth_new[,-1], 2, min)
max <- apply(ecgrowth_new[,-1], 2, max)
mean <- apply(ecgrowth_new[,-1], 2, mean)
sd <- apply(ecgrowth_new[,-1], 2, sd)
mult_mod <- lm(growth ~., data = ecgrowth_new[,-c(1,3)])
```

*** =sample_code
```{r}
# Join all statistics in a data.frame
descriptives <-

# Predict economic growth for an average country

```

*** =solution
```{r}
# Join all statistics in a data.frame
descriptives <- data.frame(min=min, max=max, mean=mean, sd=sd)
predict(mult_mod, newdata = as.data.frame(t(mean[-c(1,2)])))
```

*** =sct
```{r}
test_object("descriptives", eq_condition = "equivalent")
test_function("predict", args = c("object","newdata"))
success_msg("Great! Notice that the model's prediction for economic growth of an average country is nothing but the mean of `growth`.")
```




--- type:NormalExercise lang:r xp:100 skills:1 key:71af5cb730
## Economic Growth XIII

<div style="border: #3aaaca 3px solid">

The estimated regression equation for our extented model `mult_mod` is

$$ Growth = 0.6269 -0.0005 \times TradeShare + 1.3408 \times YearsSchool -2.1504 \times RevCoups \\\\ -0.0005 \times RGDP60 + 0.3226 \times assasinations $$ 

</div>

<br>

The model object `mult_mod` as well as the `data.frame` named `descriptives` are available in Your workspace.

*** =instructions

- Repeat the prediction from the last exercise but now assume that the country's value for $TradeShare$ is one standard deviation above the mean. <b>Hint</b>: Try to set up the `newdata` argument in Your call of `predict` using vector addition.

*** =hint

*** =pre_exercise_code
```{r}
library(foreign)
ecgrowth <- read.dta('http://s3.amazonaws.com/assets.datacamp.com/production/course_1276/datasets/Growth.dta')
ecgrowth_new <- ecgrowth[-65,]
min <- apply(ecgrowth_new[,-1], 2, min)
max <- apply(ecgrowth_new[,-1], 2, max)
mean <- apply(ecgrowth_new[,-1], 2, mean)
sd <- apply(ecgrowth_new[,-1], 2, sd)
descriptives <- data.frame(min=min, max=max, mean=mean, sd=sd)
mult_mod <- lm(growth ~., data = ecgrowth_new[,-c(1,3)])
```

*** =sample_code
```{r}
# Perform the prediction


```

*** =solution
```{r}
# Perform the prediction
predict(mult_mod, newdata = as.data.frame(t(mean[-c(1,2)] + c(0,sd[4],0,0,0))))
```

*** =sct
```{r}
test_function_result("predict")
success_msg("Correct! As expected, the prediction of economical growth now lies above its mean value.")
```
