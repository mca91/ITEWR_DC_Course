---
title       : Empirical Exercises
description : Further exercises


--- type:NormalExercise lang:r xp:100 skills:1 key:498a3c9d06
## Economic Growth I

The following exercises are considered with the subject of economical growth. Basis for this is a real data set containing growth rates from 1960 through 1995 for 65 countries and various other variables that are possible determinants of growth. 

In particular, we are interested in the relationship between growth and trade. A detailed description of the dataset can be found <a href="http://wps.pearsoned.co.uk/wps/media/objects/12401/12699039/empirical/empex_tb/Growth_Description.pdf">here</a>. 

The dataset 'ecgrowth' is available in Your workspace.

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

The datasets `ecgrowth` and `ecgrowth_new` are available in Your workspace.

*** =instructions

- For convinience, attach `ecgrowth`. Run a simple linear regression of `growth` on `tradeshare` using `lm()`. Store the result in `growth_reg`
- Use `growth_reg` to predict the growth rate for a country with a trade share of 0.5

*** =hint

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
