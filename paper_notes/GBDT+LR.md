

## Practical Lessons from Predicting Clicks on Ads at Facebook

### 1. Ranking Loss

-   NCE
-   Calibration
-   AUC

### 2. Hybrid Architecture

-   motivates by transforming real-value data by bining and cross-feature combinations, which could be well-captured by boosting trees
-   a form of ***supervised feature encoding*** 
-   concatenate leafs in each tree (each tree leaf acts as a binary value and hence a **one-vs-K encodin**g)
-   experiments' setting: limit `num_leaf = 12` in each tree 

### 3. LR Optimizer

-   Online learner SGD weight update schemas: (best -> worst)
    -   per coordinate > per weight sqrt > constant > global > per weight 
-   Compare best performance SGD scheme to BOPR 
    -   ==BOPR== : a full baysian optimzer (==Q: not understood yet : (==  )
    -   Conclusion: SGD per coordinate is comparable to BOPR

### 4. Data

#### 4.1 Streaming Negative Label Generation

-   Infrusture: online data joiner
    -   anamoly detection
-   Negative label defination: latency window size

#### 4.2 Training Data

-   Sampling methods: uniform-sampling & negative sampling (see following sessions of memory-accuracy tradeoff)

### 5. Analysis

-   Data Freshness
    -   can re-train gbdt & lr at different frequency: 
        -   *GBDT on a weekly basis, LR on a daily basis*

-   Number of estimators
    -   first 500 trees contribute most (range 1-2000 trees)
-   Boosting Feature Importance
    -   cumulative reduction on the loss function by each feature
    -   conclusion: 
        -   A small fraction of features contributes most to the accuracy -> hence tree models can *reduce \# feats to be included in sparse linear model*
        -   **Historical Features >> Contextual Features**

-   Train Data Sampling
    -   ==(NOT UNDERSTOOD) Ad CTR related: Model Re-calibration==

