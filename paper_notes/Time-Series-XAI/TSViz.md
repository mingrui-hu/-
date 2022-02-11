## 

-   Considered Architecture:
    -   CNN
-   Goal:
    -   input saliency map: identification of parts of the inputs that were responsible for a prediction
        -   per filter saliency
    -   importance of different filters
    -   filter clustering - network diversity
    -   Inverse optimization - main source of variance
    -   Robustness - adversial noise
-   Analysis:
    -   Net-work pruning based on computed importance value
-   Dataset:
    -   Regression: Traffic Dataset
    -   Anomaly Detection:
        -   SyntheticL pressure-temperature-torque with point anomalies
-   Influence 
    -   Input influence (& min-max-scaled)
    -   Filter Influence
-   Filter-clustering:
    -   hierarchical clustering with DTW as distance measure + complete linkage
        -   silhouette score to select inital number of clusters

-   Cons/Comments:
    -   lack of ==diversity of temporal signal types==
    -   no analysis on the influence score effectiveness on ==multivariate== cases where ==high correlation== may occure
    -   Architecture lacks diversity as well
    -   Does not meation about **feature importance distribution at each time step**
        -   theoritically can goes down to feature-wise score per time step based on gradient

