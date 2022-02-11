### shap

https://interpret.ml/docs/shap.html

### PDP

-   PDP function: for given value(s) of features S what the average marginal effect on the prediction is. 

    
    $$
    \hat{f_S}(x_S)=E_{X_C}[\hat{f}(x_S,X_C)]=∫\hat{f}(x_S,X_C)dP(X_C)
    $$
    $x_s$ : the specific value of the feature set(s) S that we are interested in 

    $X_C$ : the overall feature value sets C that we ignore & treated as random variables

    $\hat{f}$ : machine learning model 

-   An assumption of the PDP:  the features in **C** are **not correlated** with the features in **S**.
    -    If this assumption is violated, the averages calculated for the partial dependence plot will include data points that are very unlikely or even impossible.

-   **marginalizing out feature set $C$** 

    -   integration over the distribution of feature set C

    -   calculation approximation : Monte Carlo Sampling

        -   The partial function $\hat{f_S}$ is estimated by **calculating averages** in the training data:

        -   $$
            \hat{f_S}(x_S)=\frac{1}{n}\sum_{i=1}^n\hat{f}(x_S,x_C^{(i)})
            $$

    -   categorical features

        >   For each of the categories, we get a PDP estimate by **forcing all data instances to have the same category**. For example, if we look at the bike rental dataset and are interested in the partial dependence plot for the season, we get 4 numbers, one for each season. To compute the value for “summer”, we **replace the season of all data instances with “summer” and average the predictions**.

    -   see a numerical example in shap package `_partial_dependence.py` line 92

-   individual expectations vs partial dependencie:

    -   just as the difference between a PDP plot & the shap value scatter: the vertical distance

    >   Partial dependence plots can obscure a **heterogeneous relationship** created by interactions. PDPs can show you what the average relationship between a feature and the prediction looks like. This only works well if the interactions between the features for which the PDP is calculated and the other features are weak. In case of interactions, the ICE plot will provide much more insight.

    -   see examples in 9.1.1 -> (If) all curves seem to follow the same course, so there are no obvious interactions.

-   calculate ICE for one feature

    >   The values for a line (and one instance) can be computed by keeping all other features the same, creating variants of this instance by replacing the feature’s value with values from a grid and making predictions with the black box model for these newly created instances. 

-   cICE - centered-ICE plot
    -   Feature prediction absolute value -> feature range prediction difference
-   d-ICE - derivative ICE plot
    -    spot ranges of feature values where the black box predictions change for (at least some) instances
    -   Without interactions, the individual partial derivatives should be the same for all instances. If they differ, it is due to interactions and it becomes visible in the d-ICE plot.
    -   the **standard deviation of the derivative** helps to highlight regions in feature in S with heterogeneity in the estimated derivatives.
-   Problems:
    -    **feature distribution**:
        -   PD value of feature value with few data points is less reliable
        -   Solution: plot a rug/histogram with the PDP plot
    -   **Independence assumptions** of feature set C & S:
        -   Also, ICE curves suffer from the same problem as PDPs: If the feature of interest is correlated with the other features, then **some points in the lines might be invalid data points** according to the joint feature distribution
        -   Solution:  [Accumulated Local Effect plot](https://christophm.github.io/interpretable-ml-book/ale.html#ale): work with the **conditional** instead of the **marginal** distribution.
    -   **Heterogeneous effects might be hidden** because PD plots only show the average marginal effects. Suppose that for a feature half your data points have a positive association with the prediction – the larger the feature value the larger the prediction – and the other half has a negative association – the smaller the feature value the larger the prediction. The PD curve could be a horizontal line, since the effects of both halves of the dataset could cancel each other out.
        -   Solution: ICE plot
-   PDP-based Feature Importance
    -   the feature is not important, and the more the PDP varies, the more important the feature is
    -   It captures only the main effect of the feature and ignores possible feature interactions.
    -   feature values are given identical weights without consider feature distributions in the datasets
-   **So, a potential procedure:**
    -   calculate the correlation matrix of the input datasets
    -   if correlation is weak, then we can apply PDP feature importance happily
-   

### P:

-   In jupyter `IProgress not found`

    -   ```python
        # in notebook
        !pip install ipywidgets
        !jupyter nbextension enable --py widgetsnbextensions
        
        # then restart kernel
        ```

## Shapley value

### 1. defination

The Shapley value is the **average marginal contribution of a feature value** **across all possible coalitions**.  （like in PDP above）

-   If we estimate the Shapley values for all feature values, we get the **complete distribution of the prediction (minus the average)** among the feature values.
-   For each feature value:

​		1. average over all possible coaliations

​		2. **marginal contribution** of a feature value (not in C as well) in a certain coilation 

-   Comparision with pdp:

    -   features not in coalitaion = feature set C
    -   marginal **contribution** of a feature value in a coalition  
        -   e.g. compute the predicted apartment price **with and without the feature value** `cat-banned` and **take the differenc**e to get the marginal contribution.
        -   Similar to apply Equation (2) twice 
            -   first to feature set S = {the chosen coalition  + the interested feature value} (i.e. a feature set S with certain values $x_s$ as the instance to be explained),  feature set C drawned randomly from the background data distribution
            -   then with feature set S = {the chosen coalition}, the interested feature value will be as a r.v. as those in feature set C & drawned randomly from the background data distribution
        -   Difference from PDP -> background datasets: realistic vs synthetic:
            -   in PDP equation 2, samples(enssentially  feature set C) are exactly those in the training datasets, no **re-sampling  strategies** involved
            -   in Shapley, the way to use r.v. in feature set C in the training datasets,  is to summarize feature C distribution statistics, and generate **synthetic** background examples(ensenssentially  synthetic feature set C) as the background datasets

-   Local Interpretation

    The interpretation of the Shapley value for feature value j is: The value of the j-th feature contributed $\phi_j$ to the prediction of this particular instance compared **to the average prediction for the dataset**.

### [LIME](https://christophm.github.io/interpretable-ml-book/lime.html)

#### 1. explanation model

The recipe for training local surrogate models:

-   Select your instance of interest for which you want to have an explanation of its black box prediction.

-   Perturb your dataset and get the black box predictions for these new points.

    -   Hyperparams:`num_samples`,  `sampling_method `default: gaussian; `discretize_continuous`, etc.
    -   `lime_tabular.py` -> `LimeTabularExplainer.explain_instance() line346` --> `self.__data_inverse()`

-   Weight the new samples according to their proximity to the instance of interest.

    -   1.   caculate distance: `lime_tabular.py` -> `LimeTabularExplainer.explain_instance() line355`, by default `distance_metric='euclidean'`

        2.   define kernel `lime_tabular.py` -> `LimeTabularExplainer.__init__() line355` 
             $$
             kernel\_width = \sqrt{0.75 * num\_input\_features}
             $$
             
             $$
             kernel(d) = \sqrt{exp{-(\frac{d}{kernel\_width})^2}}
             $$

        3.   calculate neighboring_data sample weights 

             `lime_base.py` -> `LimeBase.explain_instance_with_data line 101`

        4.   used later in both feature selection & local explanation regressor (in `LimeBase`)

-   Select number of features  to be included in the local regressor

    `lime_base.py` -> 	`LimeBase.feature_selection()`	

-   Train a weighted, interpretable model on the dataset with the variations.

    `lime_base.py` -> `LimeBase.explain_instance_with_data() line 192`

    Explain the prediction by interpreting the local model.

#### **fidelity measure ?**

#### 2. number of features K

-   ==Q: so actually **one can not expect what features will be finally included in the explanation**, since its chosen by explanation model itself?==

-   -   >   

-   >    K, the number of features you want to have in your interpretable model. The lower K, the easier it is to interpret the model. A higher K potentially produces models with higher fidelity.

-   tuned through LASSO regularization term $\lambda$

    >   By retraining the Lasso models with slowly decreasing λ, one after the other, the features get weight estimates that differ from zero.

-   Other strategies are forward or backward selection of features

    -   ==like stepwise feature selection?==

    -   >   This means you either **start with the full model (**= containing all features) or with a model with **only the intercept** and then test which feature would bring the biggest improvement when added or removed, until a model with K features is reached.

-   Pertubed new local datasets

    >   For text and images, the solution is to turn single words or super-pixels on or off. 
    >
    >   In the case of *tabular* data, LIME creates new samples by perturbing each feature individually, drawing from a normal distribution with mean and standard deviation taken from the feature.

-   Defining **a meaningful neighborhood** around a point
    -   an exponential smoothing kernel 
    -   A smoothing kernel is a function that takes two data instances and returns a proximity measure. 
-   Feature Selection is preformed with **sample weights** generated from the kernel function

-   Q:

    -   for two local explanations, ==are the feature coef comparable?== i.e. are they on the same scale, since as described, the underlying model may get different regularization coef?
    -   for a single explanation, are ==the feature coefs btw different features comparable==? (since the feature importance is enssentially affected by the unit of each feature)

    -   ==may not be great for sparse / long tail categorical features?==

        >   Now note that the explanations are based not only on features, but on feature-value pairs. For example, we are saying that odor=foul is indicative of a poisonous mushroom. In the context of a categorical feature, odor could take many other values (see below). Since we perturb each categorical feature drawing samples according to the original training distribution, the way to interpret this is: if odor was not foul, on average, this prediction would be 0.24 less 'poisonous'. 

        class LimeTabularExplainer(object) --> 

        >   For categorical featues, perturb by sampling according to the train distribution, and make a binary feature that is 1 when the value is the same as the instance being explained

    -   Explanation RidgeRegression model inputs feature selection highly affected by the previous `feature_selection` step & really time costing for large number of raw input feats.
    -   ==Highly likely to loose feature interaction effects?== Since relies on the feature selected from another Ridge & then use a local model of Ridge with a very small number of features 

    -   not effecient?

