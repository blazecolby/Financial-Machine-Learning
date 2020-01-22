# Data Analysis

## Financial Data Structures
- Produce matrix X of features out of unstructured data. Unsupervised methods applied. 

Sources:
- CME
- MarketAxess


ESSENTIAL TYPES OF FINANCIAL DATA

- Fundamental: often backfilled
 - Assets, Liabilities, Sales, Costs/earnings, Macro variables
- Market Data:  all trading activity that takes place in an exchange
  - Price/yield/implied, volatility, Volume, Dividend/coupons, Open interest, Quotes/cancellations, Aggressor side
- Data Analytics:  derivative data from other 3 sources.
  - Analyst recommendations, Credit ratings, Earnings, expectations, News sentiment
- Alternative Data: data produced by individuals,  business processes, sensors.
  - Satellite/CCTV, images, Google searches, Twitter/chats, Metadat


BARS

-  Standard Bars
  - Time Bars
  - Tick Bars
  - Volume Bars
  - Dollar Bars
  
-  Information-Driven Bars
  - Tick Imbalance Bars
  - Volume/Dollar Imbalance Bars
  - Tick Runs Bars
  - Volume/Dollar Runs Bars
  
Events that alter the nature of the time series under study need to be treated properly i.e.
- model spreads with changing weights
- baskets that must be rebalanced
- Index's constituents are changed
- Replace an expired contract with another
- Manipulating futures

DEALING WITH MULTI-PRODUCT SERIES

ETF Trick

- Multiple securities represented as one cash product.
- Single dataset that resembles a total-return ETF.
- Assumes you only trade cashlike products.(Non-expiring)

Ex. Strategy that trades a spread of futures:
- Spread represents weights that change over time.
- Spread may converge even if prices do not change.
  - Series may be misled to believe PnL(net mark-to-market value of profits and losses) resulted from weight-induced convergence.
  - Spreads can acquire negative values, because they do not represent a price.
  - Trading times won't align exactly for all constituents; not always tradeable at last levels published, or w/ zero latency risk

(Series to be used to model, generate signals, and trade as if it were an ETF):
- Create series that shows value of 1$ invested in a spread.
- Changes in series reflect changes in PnL
  - Strictly positive

PCA Weights

Many ways to to compute hedging weights.


Single Future Roll


SAMPLING FEATURES
- Sampling continuous, homogeneous, and structured dataset from a collection of unstructured financial data.
  - Don't apply ML algorithm yet.
    - Several ML algorithms don't scale well
    - Achieve best accuracy on relevant examples. Predict +/- signs for return. Predict +/- signs after catalyic event will be better.
    
Sampling bars to produce a features matrix with relevant training examples:

Sampling for Reduction
- Use downsampling to reduce number of features needed to fit a model.

Event-Based Sampling
- Use events as a proxy to reducing the number of relavent features.
- Events may be related to macro stats; spike in volatility, sizable departure in spread from equilibrium. 
- Event can be characterized as significant and let ML learn whether there is a accurate prediction function from those circumstances or not. If not, then the characterization of significance changes. 

The CUSUM Filter: quality control method
- detects shift in mean value of measured quantity from target value.


## Labeling
- Methods for labeling in order to use supervised methods.
 
FIXED-TIME HORIZON METHOD
- Uses time bars. Time bars do not exhibit good statistical props. 
 - Label w/ varying threshold. Estimated w/ a rolling exponentially weighted std of returns.
 - Use Volume or dollar bars, as their volatilities are much closer to constant (homoscedasticity).
 - Account for missing path followed by prices (i.e. doesn't account for stopping-out).
 
COMPUTING DYNAMIC THRESHOLDS
- Set profit taking and stop-loss limits that are a function of risks in a bet. 
- Compute daily volatility estimates at intraday estimation points. 

- Use output of function to set default profit taking/stop-loss limits through rest of chapter.

TRIPLE-BARRIER METHOD: Label observation according to first barrier touched out of three barriers.
- Set two horizontal barriers and one vertical barrier.
- Horizontals = profit-taking and stoploss limits, dynamic function of estimated volatility.
- Vertical = bars elapsed since position was taken (expiration).
 - upper barrier: 1
 - lower barrier: -1
 - vertical barrier: 0
 
Useful configurations:
 - (1,1,1): realize profit w/ max tolerance for losses and holding period.
 - (0,1,1): exit after number of bars unless stopped-out.
 - (1,1,0): take profit if we're not stopped-out.
 Less useful configurations:
 - (0,0,1): equivalent to fixed-time horizon method. Apply to volume/dollar/info-bars.
 - (1,0,1): held until profit or max period met. Disregard intermediate realised losses. 
 - (1,0,0): hold to profit.
 Illogical configurations:
 - (0,1,0): hold until stopped-out
 - (0,0,0): position locked forever.

LEARNING SIDE AND SIZE
- Use when there is no model to find sign. i.e. symmetric/no horizontal barriers.

META-LABELING
- Suppose you have a model that provides the sides(long, short) but not size(amount to bet). 
- Build secondary model that learns to use primary exogenous model; like a decorator.
- Create variables that contains sides of bet, now it's possible to descriminate b/w profit taking and stop loss.

- Binary label created(bet or pass), then size is derived. 
- Binary classification problems present a trade-off b/w type-1/2 errors. 
- Increase TP = Increase FP
- ROC shows the cost of increasing TP
- ( Precision: TP / TP + FP ) ( Recall: TP / TP + FN )
- F1-score: efficiency of classifier as the harmonic average b/w Precision & Recall.

THE QUANTAMENTAL WAY
- The features used by such meta-labeling ML algorithm could range from market information to biometric statistics to psychological assessments. 
- meta-labeling offers a clear path to the the quantamental way

DROPPING UNNECESSARY LABELS
- Drop rare labels.

## Sample Weights
- In finance, observations are not generated by independent and identically distributed (IID) processes.



