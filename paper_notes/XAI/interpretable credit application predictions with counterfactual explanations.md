## Introduction

- argues cons of counterfactual:

  1. Lack of feature sparsity
  2. do not consider dataset' (i.e. global) feature importance

- Two **weighting strategies** when generating explanations

  - goal: to promote more compact explanations
  - global feature importance
  - KNN
  - **add to loss function distance term**

- Loss function

  - $$
    L(x, x', y',λ) = λ(fˆ(x') − y')^2 + d(x, x')
    $$

- Optimization: **Nelder-Mead algorithm**  

- Positive counterfactual interpretations: **safety margin** from the decision boundary

  - How much was I accepted by ?
  - consider feature importance and **value range**
  - By setting the target $y'$ to be the decision boundary $P(y=1)=0.5$

- Do not evaluate faithfulness & fairness
- 可以借鉴他们的可视化形式
  - ![image-20220301160455738](interpretable%20credit%20application%20predictions%20with%20counterfactual%20explanations.assets/image-20220301160455738-16461218972581.png)