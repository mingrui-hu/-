

### 

Section 3.5

-   Properties of Explanation Methods
    -   Expressive power:
        -   IF_THEN rules, decision trees,  a weighted sum, natural language or something else
    -   Translucency & Portability:
        -   Model Intrinsic <--> Mode agnostic
    -   Algorithmic Complexity
-   Properties of Individual Explanations
    -   Accuracy : importance depending on **the goal of the explainer**: to take place of an ml algo, or just to explain an ml algo
    -   Fidelity: may be local fidelity(e.g local surrogate model or shapley values)
    -   Consistency: of explainations of different models trained on the same task and produce very similar results --> tricky --> Rashonmon Effect(different features, but similar predictions)
    -   Stability: similar explanations for similar instances
        -    <- can be caused by an non-deterministic components of the explanation method, such as data sampling
    -   Comprehensibility
    -   **==Certainty==**
    -   Degree of (feature/parts) Importance
    -   Novelty: data distribution --> how far a new data instance is away from the training dataset distribution
        -   may related to certainty -> higher novelty shall indicates high uncertainty
    -   Representativeness

### Section 9.3 Counterfactual

#### 9.3.1 Generating Counterfactual Examples

-   loss function $L(instance \space of \space interest, a\space counterfactual,  desired\space output\space y^\prime)$
-   find the counterfactual explanation that minimizes this loss using an optimization algorithms

##### 9.3.1.1 Method by Wachter et al. (2017)

-   introduced counterfactual explanation as an interpretation method

-   balance requirements::

    -    the prediction for the counterfactual matches the desired outcome 
    -   the counterfactual similar to x

-   $$
    L(x, x^\prime, y^\prime, \lambda) = \lambda\cdot(\hat{f}(x^\prime) - y^\prime)^2 + d(x, x^\prime)
    $$

-   $\lambda\cdot(\hat{f}(x^\prime) - y^\prime)^2$: quadratic distance between model prediction for counterfactual $x^\prime$ and the desired output $y^\prime$

-   $d(x, x^\prime)$: defined as Manhatten distance weighted the inverse median absolute deviation (MAD) of each feature:
    $$
    d(x, x^\prime) = \sum_{j=1}^p\frac{|x_j - x^\prime_j|}{MAD_j}
    $$

​       i.e. the (weighted) absolute differences between instance $x$ and counterfactual $x^\prime$
$$
MAD_j = \text{median}_{i\in{}\{1, \ldots, n\}}(|x_{i,j}-\text{median}_{l\in{}{1, \ldots, n}}(x_{l, j})|)
$$

-   instead of set  $\lambda$ as hyperparameter, set a constraint with tolerance $\epsilon$ and treat $\lambda$ as a learnable parameters
    $$
    |\hat{f}(x^\prime) - y^\prime|\leq\epsilon
    $$
    

-   optimation methods:
    -   ==Nelder-Mead==
    -   gradient-based methods

-   local optimal counterfactual $x^\prime$ found: 
    -   increading $\lambda$ untila a sufficient close solution is found( $i.e. L\leq \lambda$)

$$
\arg\min_{x^\prime}\max_{\lambda}L(x, x^\prime, y^\prime, \lambda)
$$

##### 9.3.1.2 Method by Dandl et al.(2020)

-   Loss function
    $$
    L(x, x^\prime, y^\prime, \lambda) = \big(o_1(\hat{f}(x^\prime), y^\prime), o_2(x, x^\prime), o_3(x, x^\prime), o_4(x^\prime, X^{obs})\big)
    $$
    

-   $o_1(\hat{f}(x^\prime), y^\prime)$: 

    -   prediction of counterfactual $x^\prime$ should be as close as possible to our desired prediction $y^\prime$

    -   Manhattan metric ($L_1 \space norm$)

    -   $$
        o_1(\hat{f}(x^\prime), y^\prime) = \begin{cases}0&\text{if $\hat{f}(x') \in y'$}
        $$

    -   $$
        
        $$

    -   

