---
title       : Heteroskedasticity
description : Insert the chapter description here

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:35167f113b
## Violation of OLS Assumptions

Have a look at the plot that showed up in the viewer to the right. Which of the OLS assumptions could be possibly violated?

*** =instructions
- No perfect multicollinearity
- Homoskedasticity
- Outliers are seldom
- Y is $\chi^2_{11}$ distributed

*** =hint
Have a look at the plot. What can you say about the dispersion of observations?

*** =pre_exercise_code
```{r}
library(sandwich)

set.seed(1)
x <- runif(500, 0, 1)
y <- 5 * rnorm(500, x, x)
plot(y ~ x, col = "steelblue", pch = 19)
```

*** =sct
```{r}
msg_bad <- "That is not correct!"
msg_success <- "Exactly! There seems to be heteroskedasticity: Dispersion increases with x."
test_mc(correct = 2, feedback_msgs = c(msg_bad, msg_success, msg_bad, msg_bad))
```