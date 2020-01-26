# Backtesting 

## Bet Sizing
 - If you don't size your bets properly, your investment strategy will inevitably lose money.
 - Sizing bets may be done through ML predictions.

STRATEGY-INDEPENDENT BET SIZING APPROACHES
- We would prefer to size positions in such way that we reserve some cash for the possibility that the trading signal strengthens before it weakens.
  - Compute series where the number of concurrent long bets at a given time is the number of concurrent short bets at the same time. 
  - Bet concurrency is derived for each side. 
  - Fit a mixture of two Gaussians. Then bet size is derived. 
  - Stronger the signal the greater the bet size. 
- Budgeting approach.
  - Compute max number of concurrent long bets and max number of concurrent short bets. 
  - Derive bet size. 
  - Max bet not reached before last signal is triggered. 
- Meta-labelling
  - Fit classifier to determine probability of missclassification, then use probability to get bet size.
    - Independent of primary model.
      - allows for use of features predictive of false positive.
    - Predicted probability may be directly translated to bet size. 
    
AVERAGING ACTIVE BETS
- All bets are associated w/ a holding period; time originated to first barrier touch. 
- The idea is to average all sizes across all bets still active at a given time. 

SIZE DISCRETIZATION
- Averaging removes some excess turnover w/ excess being undesirably small bets. 
- Discretization allows for minimizing excess turnover. 

DYNAMIC BET SIZES AND LIMIT PRICES
- Adjust bet sizes as market prices and forecast prices fluctuate. From this, order limit price will be derived.
- 

## Dangers of Backtesting

## Backtesting through Cross-Validation

## Backtesting on Synthetic Data

## Backtest Statistics

## Understanding Strategy Risk

## Machine Learning Asset Allocation





Let's take a look at three common areas in the general machine learning process in finance, then pick out one common mistake from each of these areas. The areas are data processing, data classification, and data evaluation. By viewing these common problems one may preview both the mistake and the solutions claim. Arguably inherent in each solutions claim is its' explainability.

1) Data processing introduces fractional differentiation, which solves the problem of integer differentiation.
2) Classification introduces meta-labeling, which solves the problem of learning side and size simultaneously.
3) Evaluation introduces purging and embargoing, which solves the problem of cross-validation leakage. 

Overshadowing and complementing the aforementioned solution claims and problems is that explainability is an extension of the ability of a financial investment research team to come up with logical investment strategies.







