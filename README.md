# CLogitBoost
Boosting for Conditional Logistic Regression

This repository contains code for the family CLogit() that can be used within the R-package mboost. It provides the option to use mboost for boosting conditional logistic regression, which can be applied both to matcehd case-control studies and to discrete choice data. Beside the family itself, the repository contains a function (make.cv.folds) that can be used for cross-validation of models estimated via CLogit(). Here, the subsets in cross-validation need to be created while respecting the strata. 
