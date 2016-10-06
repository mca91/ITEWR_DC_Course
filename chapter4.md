---
title       : GMT
description : Insert the chapter description here

--- type:MultipleChoiceExercise lang:r xp:100 skills:1 key:726a6d460b
## The Gauss Markov Theorem I

Suppose you got the regression model

$$ y_i=b_0 $$

i.e. a regression of some variable $y_i$ solely on a constant or, put differently, the regressor is a values of ones

$$\mathbf{X} = (1 \dots 1)'$$

In the plotting area on the right you see the result of a Monte Carlo simulation analysing distributional properties of the OLS estimator for $ \beta $ in the model above and another linear estimator $\overset{\sim}{\beta}$ which uses different weights than OLS. Say, $\beta=0$. Is the result consistent with what you expect beeing aware of the Gauss-Markov Theorem?  

*** =instructions
- Yes, both estimators seem to be unbiased but the OLS estimator has less dispersion.
- No, the distribution of $\overset{\sim}{\beta}$ looks more like a standard normal distribution.
- Cannot be answered without prior inspection of data.

*** =pre_exercise_code
```{r}
# Set sample size and number of repititionas

n <- 100      
reps <- 1e5

# Choose epsilon and create a vector of weights as defined above

epsilon <- 0.8
w <- c( rep((1+epsilon)/n,n/2), rep((1-epsilon)/n,n/2) )

# Draw random sample y_1,...,y_N from the standard normal distribution 
# Compute both estimates 1e6 times and store the result in vectors  

ols <- rep(NA,reps)
weightedestimator <- rep(NA,reps)

for (i in 1:reps)
{
  y <- rnorm(n)
  ols[i] <- mean(y)
  weightedestimator[i] <- crossprod(w,y)
}

# Plot estimates of the estimators distribution 

plot(density(ols),col="purple", lwd=3, main="Density of OLS and Weighted Estimator",xlab="")
lines(density(weightedestimator),col="steelblue", lwd=3) 
abline(v=0,lty=2)
legend('topright', c("OLS","weighted"), col=c("purple","steelblue"),lwd=3)
```
*** =sct
```{r}
msg_bad <- "That is not correct!"
msg_success <- "Exactly!"
test_mc(correct = 1, feedback_msgs = c(msg_success, msg_bad, msg_bad))
```