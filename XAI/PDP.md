https://christophm.github.io/interpretable-ml-book/pdp.html

https://github.com/interpretml/interpret

-   Global Model-Agnostic Model

    >   A partial dependence plot can show whether **the relationship between the target and a feature** is linear, monotonic or more complex.

    >    For example, when applied to a **linear regression** model, partial dependence plots **always** show **a linear relationship**.

    >   The partial dependence plot is a **global** method: The method **considers all instances** and gives a statement about the global relationship of a feature with the predicted outcome.
    -   sensitive to outliers if the assumption 

        >   features in C are not correlated with the features in S
    
        is violated.

-    PDP for regression : def

    -   marginalise predictions over other features $X_C$

        $ \hat{f}_S(x_S) = E_{X_C}[\hat{f}_S(x_S, X_C)] = \int{\hat{f}_S(x_S, X_C)} dP(X_C) $

        

    -   Estimate $\hat{f}_S(x_S)$: Monte Carlo Method

        $\hat{f}_S(x_S) = \frac{1}{n}\sum_{i=1}^n$

    -   >   Usually, there are only one or two features in the set S

-   PDP for categorical features(==??Q==)

    >   For each of the categories, we get a PDP estimate by forcing all data instances to have the same category. For example, if we look at the bike rental dataset and are interested in the partial dependence plot for the season, we get 4 numbers, one for each season. To compute the value for “summer”, we ==replace the season of all data instances with “summer”== and average the predictions.

-   PDP importance
    -   Motivation: pdp plot flat -> not important; vice versa.
    -   Numerical features:
        -   importance is defined as **the deviation of each unique feature value from the average curve**
    -   Categorical features:
        -   **the range rule**: the range of the PDP values for the unique categories divided by four

-   Cons:
    -   It captures only the main effect of the feature and *ignores possible feature interactions*. 
    -   defined over the unique value, *ignore the value counts* and give same weight to all values.

