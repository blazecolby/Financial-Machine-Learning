Data Analysis

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






