---
title       : Empirical Exercises
description : Further exercises


--- type:NormalExercise lang:r xp:100 skills:1 key:498a3c9d06
## Economic Growth I

The following exercises are considered with the subject of economical growth. Basis for this is a data set containing growth rates from 1960 through 1995 for 65 countries and various other variables that are possible determinants of growth. In particular, we are interested in the relationship between growth and trade. A detailed description of the dataset can be found <a href="http://wps.pearsoned.co.uk/wps/media/objects/12401/12699039/empirical/empex_tb/Growth_Description.pdf">here</a>. 

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

Have a closer looked at the scatterplot. Does there appear to be any relationship between the variables?


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
