PART 1 DATA ANALYSIS
- Financial Machine Learning as a Distinct Subject
- Financial Data Structures
- Labeling 
- Sample Weights
- Fractionally Differentiated Features

PART 2 MODELLING
- Ensemble Methods
- Cross-Validation in Finance
- Feature Importance
- Hyper-Parameter Tuning with Cross-Validation

PART 3 BACKTESTING
- Bet Sizing
- The Dangers of Backtesting
- Backtesting through Cross-Validation
- Backtesting on Synthetic Data
- Backtest Statistics
- Understanding Strategy Risk
- Machine Learning Asset Allocation

PART 4 USEFUL FINANCIAL FEATURES
- Structural Breaks
- Entropy Features 
- Microstructural Features

PART 5 HIGH-PERFORMANCE COMPUTING RECIPES
- Multiprocessing and Vectorization
- Brute Force and Quantum Computers
- High-Performance Computational Intelligence and Forecasting Technologies

___ 

I'm going to throw a wrench in my previous thesis, on which explainability was set on a basis of two main things, one was on an individuals ability to understand the why of a problem and the second was on an individuals ability to fully articulate a model between the points of x and y. There may be a caveat to this. And that is that AI doesn't necessarily need to tell the truth, it just needs to be able to tell a convincing story. The understanding is not just about having to pin down a machine learning algorithm and corner it in order to understand what is going on. Understanding is about being able to convince ourselves that a story is true. I don't bring this up to stray away from the true why, but to add further explaination to the why. The why is multifaceted. It is the tie between the final product, the functional mechanisms, and the raw materials. And the understanding that the truth may not be the truth, but merely an extremely convincing story. 

Success = systemization
Discretionary PMs work in silos and may make team work more difficult.
Meta strategy paradigm: the only true alpha left is microscopic.

Production chain:
- Data Curators
- Feature Analysts
- Strategists
- Backtesters
- Deployment Team
-- Portfolio Oversight
- Embargo
- Paper trading
- Graduation
- Re-allocation
- Decommission

New variations run with old.


Many investment managers believe that the secret to riches is to implement an extremely complex ML algorithm.

Challenges involved in developing a successful investment strategy:
- Data: Garbage in, garbage out.
  - Work with unique hard-to-manipulate data.
  - Structure correctly, create informative labels, model non-IID series correctly, find predictive features.
- Software: Custom task needs custom tools. Popular libs = lots of competition. 
  - Develop your own classes. 
- Hardware: Heavy computation.
  - Become HPC expert.
  - Structure code that can be parallel. Develop algorithms for quantum computers.
- Math: proofs take a long time. 
  - Solve problems by experiment, i.e. Bailey, Borwein and Plouffe (1997) found spigot algo for pi w/o proof.
  - Use memory-preserving data transformations, experimental methods more reliable than backtests, rely on expiremental methods to lead research, structural break methods, queuing methods, discrete methods.
- Meta-Strategies: Amateurs develop individual strategies.
  - professionals develop methods to mass-produce strategies, methodic hard work
  - build research process that finds features across classes, while dealing with multi-collinearity. Combine  predictions into a one bet.
- Overfitting: standard CV fails in finance.
  - Be cognizant of overfitting.
  - Use 3 provided backtest methods, quantify amount of overfit, learn robust techniques. 

Explainability is paramount in financial machine in order to have success. 

Econometrics is the application of classical statistical methods to economic and financial series. Standard econometric models do not learn. Overly simplistic. Econometrics may be good enough to succeed in financial academia (for now), but succeeding in business requires ML.

Financial ML methods do not replace theory. They guide it.

Framework-specific approaches need to be developed. That is the focus of this book.

Backtest overfitting is our equivalent to “P versus NP”.

U.S. National Laboratories are among the research centers with the longest track record and experience in using ML. 


When looking at machine learning in finance, reading Advances in Financial Machine Learning by Marcos Lopez De Prado is a good place to start. This is a good source for explainability in a domain specific context due to the fact that most, if not all, of the information in the book is based on both academic rigor and practicality through application from AUM. 

When we look at a deep learning model and we take an algorithm like lime or like Shap values, we are essentially taking an abstraction of the inner workings of a model. Each algorithm giving a slightly different interpretation or perspective on the data from that model. When we look at these examples they are domain agnostic, and therefore add a layer of abstraction away from the nuances that may come from explainability from a specific domain or a specific exmample.

It's important to reiterate that interpretability is different than explainability, and that not all explainable models are interpretable. 

Let's dive in to some examples from De Prado to get a better sense of this. 

First, let's go straight to the meat on the bone, the black box. 

We can further pin down the black box by looking at feature importances. Notably, understanding feature importance opens up the proverbial black box.

- We can gain insight into the patterns identified by the classifier if we understand what source of information is indispensable to it. 

Yes, the algorithm has learned without us directing the process.
- But that does not mean that we cannot (or should not) take a look at what the algorithm has found.
    - This in and of itself is what explainability is. Finding any means possible to better understand what's happening and what's being said of an ml algorithm. 
    
Once we know what features are important, we can learn more by running expirements. 
Here are some examples of questions/expirements provided by Prado:
- Are these features important all the time, or only in some specific environments? 
- What triggers a change in importance over time? Can those regime switches be predicted?
- Are those important features also relevant to other related financial instruments?
- Are they relevant to other asset classes?
- What are the most relevant features across all financial instruments?
- What is the subset of features with the highest rank correlation across the entire investment universe?

"Backtesting is not a research tool. Feature importance is."
- " Marcos Lopez de Prado "
- Advances in Financial Machine Learning (2018)
