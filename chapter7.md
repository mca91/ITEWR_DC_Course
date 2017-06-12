---
title       : Empirical Exercises
description : Further exercises


--- type:NormalExercise lang:r xp:100 skills:1 key:498a3c9d06
## Economic Growth I

The following exercises are considered with the subject of economical growth. Basis for this is a data set containing growth rates from 1960 through 1995 for 65 countries and various other variables that are possible determinants of growth. In particular, we are interested in the relationship between growth and trade. A detailed description of the dataset can be found <a href="http://wps.pearsoned.co.uk/wps/media/objects/12401/12699039/empirical/empex_tb/Growth_Description.pdf">here</a>. 

The dataset 'ecgrowth' is available in Your workspace.

*** =instructions

- Create a scatterplot of average annual growth ('growth') on the average trade share ('tradeshare').

*** =hint

Use the 'plot' function.

*** =pre_exercise_code
```{r}
library(foreign)
ecgrowth <- read.dta('Growth.dta')
```

*** =sample_code
```{r}
# plot the data
```

*** =solution
```{r}
#plot the data
plot(ecgrowth$growth, ecgrowth$tradeshare)
```

*** =sct
```{r}

```
