# CLogitBoost
Boosting for Conditional Logistic Regression

This repository contains code for the family CLogit() that can be used within the R-package mboost. It provides the option to use mboost for boosting conditional logistic regression, which can be applied both to matcehd case-control studies and to discrete choice data. Beside the family itself, the repository contains a function (make.cv.folds) that can be used for cross-validation of models estimated via CLogit(). Here, the subsets in cross-validation need to be created while respecting the strata. 
```
# get all required packages 
require("devtools")
devtools::install_github("Schaubert/ClogitTree")
library(CLogitTree)
require(survival)
require(mboost)


# load functions required for CLogitBoost
source("https://github.com/Schaubert/CLogitBoost/blob/main/CLogit.R")

# get illustrative data
data("illu.data")
illu.data$resp <- cbind(illu.data$y, illu.data$strata)

# fit CLR using clogit
clr <- clogit(y~x+Z1+Z2+Z3+Z4+Z5+strata(strata), data = illu.data)
summary(clr)

# fit CLR using gamboost
boostclr <- gamboost(resp ~ bols(x) + bols(Z1) + bols(Z2) + bols(Z3) + 
                       bols(Z4) + bols(Z5), data = illu.data, family = CLogit(),
                     control = boost_control(mstop = 5000))

boostclr2 <- gamboost(resp ~ bols(x, intercept = FALSE) + bols(Z1, intercept = FALSE) + 
                       bols(Z2, intercept = FALSE) + bols(Z3, intercept = FALSE) + 
                       bols(Z4, intercept = FALSE) + bols(Z5, intercept = FALSE), data = illu.data, family = CLogit(),
                     control = boost_control(mstop = 5000))

# compare estimated coefficients
coef(boostclr)
coef(boostclr2)
coef(clr)
```
