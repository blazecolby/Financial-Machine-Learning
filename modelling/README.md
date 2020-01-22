Explain what makes them effective, and how to avoid common errors that lead to their misuse in finance.

# Modelling

## Ensemble Methods

SOURCES OF ERRORS
- Bias
- Variance
- Noise
 
Ensemble methods combine sets of weak learners, based on same algorithm, to create a stronger learner.  
 
BOOTSTRAP AGGREGATION(BAGGING)

Generate training datasets by random sampling with replacement.
Fit estimators, one on each training set. (Can be fit in parallel)
Ensemble forecast is the simple average of the individual forecasts.

BOOSTING
- Generate one training set by random sampling with replacement.
- Fit one estimator using that training set
- If estimators accuracy is greater than the acceptance threshold, estimator is kept.
- Give more weight to misclassified observations, and less weight to correctly classified observations.
- Repeat previous steps until N estimators are produced.
- The ensemble forecast is the weighted average of the individual forecasts from the N models, where the weights are determined by the accuracy of the individual estimators. AdaBoost is one of the most popular.

BAGGING VS. BOOSTING IN FINANCE
- Individual classifiers are fit sequentially.
- Poor-performing classifiers are dismissed.
- Observations are weighted differently in each iteration.
- The ensemble forecast is a weighted average of the individual learners.

BAGGING FOR SCALABILITY
- Build bagging algorithm where base estimator belongs to class that doesn't scale well with sample size.
- When defining that base estimator, we will impose a tight early stopping condition.
  - sklearn’s SVM:  set a low value for the max_iter parameter, say 1E5 iterations.
  - Could also raise tolerance level through parameter 'tol'
  - Number of levels in an RF (max_depth)
  - Minimum weighted fraction of the sum total of weights in an RF to be at leaf node.
- Use Parallel Processing for bagging
  
## Cross-Validation in Finance
- Standard CV fails in finance.

GOAL OF CROSS-VALIDATION
  
  
  
  
