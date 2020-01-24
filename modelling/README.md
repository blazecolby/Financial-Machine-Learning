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
- Build a more robust model.

- Observations cannot be assumed to be drawn from an IID.
 - Leakage takes place when the training set contains information that also appears in the testing set. 
 
- Testing set is used multiple times in the process of developing a model.

PURGED K-FOLD CV
- Purging: purge train set observations whose labels overlap in time with labels included in test set.
- Embargo: eliminate training set observations that immediately follow an observation in the test set.

## Feature Importance
- Common mistake:
 - Take some data, run it through an ML algorithm, backtest predictions, repeat sequence until nice-looking backtest shows.
 
- The fact that we are repeating a test over and over on the same data will likely lead to a false discovery. 
- Typically takes about 20 iterations to discover false investment strategy, based on significance, false positive rate of 5%.
 - This is a waist of time and money. 
 - Feature importance offers an alternative.

THE IMPORTANCE OF FEATURE IMPORTANCE

- It's really easy to overfit a backtest.

- analyses that must be performed before any backtest is carried out.

- Understanding feature importance opens up the proverbial black box.
 - Gain insight to patterns identified by classifier if we understand what source of info is indispensable.
 - Algorithm has learned without us directing the process.
 - That doesnt mean we cant/shouldn't take a look at what the algorithm has found.
 
 
 Backtesting is not a research tool. Feature importance is.
 
 Learn by conducting experiments with feature importance. 
 - Are these features important all the time, or only in some specific environments?
 - What triggers a change in importance over time?
 - Can those regime switches be predicted?
 - Are those important features also relevant to other related financial instruments?
 - Are they relevant to other asset classes?
 - What are the most relevant features across all financial instruments?
 - What is the subset of features with the highest rank correlation across the entire investment universe?
 
- Distinguish between feature importance methods based on whether they are impacted by substitution effects.
- Substitution takes place when estimated importance of one feature is reduced by presence of other related features

- Substitution effects = multi-collinearity (reduce with PCA)
 - Multi-collinearity = inter-associations among the independent variables.
 
- Mean decrease impurity (MDI), (fast) (only tree classifiers)
 - is an explanatory-importance (in-sample, IS) method:
  - Each node in each decision tree (dt), selected feature splits to subset so impurity is decreased. 
  - Can derive for each dt, amount of overall impurity decrease can be assigned to each feature. 
  - Can average values across all estimators and rank features accordingly.
   - Masking effects occur when some features systematically ignored by tree. 1 feature considered p/ level.
   - (IS) Every feature will have some importance, even if they have no predictive power whatsoever.
   - Can't be generalized to non-tree classifier
   - Doesn't address substitution effects. 
   - Biased towards some predictor variables.

- Mean decrease accuracy (MDA): (slow) (any classifier)
 - Predictive-importance (out-of-sample, OOS) method.
  - Fit classifier.
  - Derive performance OOS based on performance score.
  - Permutates each column of feature matrix.
  - Importance of feature is a function of loss in performance caused by column’s permutation.
   - Not limited to accuracy as sole performance metric.
   - Susceptible to substitution effects in presence of correlated features. Makes two identical features irrelevant
   - May conclude all features as unimportant.


FEATURE IMPORTANCE WITHOUT SUBSTITUTION EFFECTS
- Substitution tends to remove important features that happen to redundant. May lead to bad assumptions. 

- Single Feature Importance (SFI): (complement to MDI & MDA)
 - cross-section predictive-importance (OOS) method.
  - Compute OOS performance score of each feature in isolation.
   - Can be applied to any classifier.
   - Not limited to accuracy.
   - No substitution effects take place,since only one feature is taken into consideration at a time.
   - Can conclude all features are unimportant, because performance is evaluated via OOS CV.
  - SFI Limitation is classifier w/ two features can perform better than bagging of two single-feature classifiers.
   - Joint effects and hierarchical importance are lost in SFI.
   
- Orthogonal Features
 - Substitution effects dilute the importance of features mea- sured by MDI.
 - Underestimate the importance of features measured by MDA.
- Partial solution is to orthogonalize features.
- PCA minimizes orthogonalization

PARALLELIZED VS. STACKED FEATURE IMPORTANCE
-  Two research approaches to feature importance:
 - PARALLELIZED:
 - For each security in an investment universe, form a dataset and derive the feature importance in parallel.
  - Important features across a variety of instruments are more likely to be associated with underlying phenoma.
   - Particularly when feature importances exhibit high rank correlation across criteria.
   - Fast (parallizable).
 - STACKED: (computationally expensive)
 - Stack all datasets into one dataset. 
  - Distributional homogeneity = importance across all instruments simultaneously.
  - Classifier fit on larger dataset.
  - Importance is derived directly, weighting scheme not needed for combining results.
  - More general and less biased. 
  - Because importance scores aren't averaged, substitution effects aren't minimized.

-- Technique for expanding classes:
  - super() class extends base functionality of another class. Enables use of another classes methods. 

## Hyper-Parameter Tuning with Cross-Validation
- essential step in fitting. 
 - Special attention is placed on cross-validating any tuned hyper-parameter.
 - Purged k-fold CV may be used to tune hyper-parameters.
 
GRID SEARCH CROSS-VALIDATION
- Conducts exhaustive search for combination of parameters that maximizes CV performance.
 - Reasonable first approach if you don't know the underlying structure of data. 
 
RANDOMIZED SEARCH CROSS-VALIDATION
- For algorithms that have larger number of parameters.
- Random sample CV

- Log-Uniform Distribution (do not respond linearly) == logarithm of draws is uniformly distributed.
- Some algorithms only accept non-negative hyper-parameters.
 - C in SVC classifier
 - Gamma in RBF kernel 

SCORING AND HYPER-PARAMETER TUNING (Log loss/Cross-entropy loss/Logistic regression loss):
- neg_log_loss for scoring in financial ML applications is better. 
- Accuracy is equal for a bad buy prediction w/ high probability & for a bad buy prediction with a low probabiliy. 
- Accuracy can offset a miss with a high probability with a hit with a low probability.

- CV scores classifier w/ sample weights.
- Observation weights are a function of the observations absolute return. 
- This implies that that log loss estmates the classifiers performance in terms of variables involved in PnL.
--
- Correct:
 - Label for side.
 - Probability for position size.
 - Sample weight for observations return.
 


 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
