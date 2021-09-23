

# XGBOOST

## Summary

1. Scalabity
   - weighted quantile sketch for efficient proposal calculation(instance weight, approximating tree learning)
   - sparsity-aware algorithm for sparse data $\rightarrow$ parallel tree learning
   - cache-aware block structure for out-of-core learning
2. Regularized Objective

### Regularized objective

- Consideration: easy to parallel computation
  $$
  L(\phi) = \sum_il(\hat{y_i}, y_i) + \sum_k\Omega(f_k)
  \\
  where \space \Omega(f) = \gamma T + \frac{1}{2}\lambda ||w||^2
  $$

- downgrade to tranditional gbdt if $\lambda$ and $\gamma$ set to 0

- **Loss at the t-th iteration**

  - greedily add the $f_t$ that most improves our model

  $$
  L^{(t)} = \sum_{i=1}^nl(y_i, \hat{y_i}^{(t-1)} + f_t(\bold{x}_i)) + \Omega{f_t}
  $$

  - second order approximation [12]
    $$
    L^{(t)} \approx \sum_{i=1}^n[l(y_i, \hat{y}^{(t-1)}) + g_if_t(\bold{x}_i) + \frac{1}{2}h_if_t^2(\bold{x}_i)] + \Omega(f_t) \\
    where \\
    g_i = \partial_{\hat{y}^{(t-1)}}l(y_i, \hat{y}^{(t-1)})\\
    
    h_i = \partial^2_{\hat{y}^{(t-1)}}l(y_i, \hat{y}^{(t-1)})
    $$

  - remove constant terms
    $$
    \tilde{L}^{(t)} = \sum_{i=1}^n[g_if_t(\bold{x}_i) + \frac{1}{2}h_if_t^2(\bold{x}_i)] + \Omega(f_t)
    $$
    
  - expand $\Omega$
  
    ![image-20210922160440635](D:\笔记\paper_notes\xgboost.assets\image-20210922160440635-16322978828002.png)
  
    - 所有样本 $\sum_{i=1}^n$ 等于 所有叶子节点$\sum_{j=1}^T$中的样本之和$\sum_{i\in I_j}$
    - $f_t \rightarrow \sum_{j=1}^Tw_j$ 
  
  - For a fixed structure $q(\bold{x})$, optimal weight $w_j^*$ of leaf j:
  
    ![image-20210922160858938](D:\笔记\paper_notes\xgboost.assets\image-20210922160858938-16322981402963.png) 
  
    叶子结点所有样本的一阶导之和/(二阶导之和 + $\lambda$)
  
  - then the optimal loss $\rightarrow$: ==scoring function to measure quality of a tree structure q==
  
    similar to **impurity score** for evaluating decision trees
  
    ![image-20210922161012692](D:\笔记\paper_notes\xgboost.assets\image-20210922161012692-16322982140444.png)
  
- Evaluating split candidates $\rightarrow$ split structure score

  ![image-20210922160236465](D:\笔记\paper_notes\xgboost.assets\image-20210922160236465-16322977583861.png)

#### shrinkage

#### column (feature) subsampling

## 3. Split finding algorithm

- exact greedy algorithm: 

  - enumerate all possible splits over all the features

  - computationally demanding for ***continuous*** features

    ![image-20210922162014992](D:\笔记\paper_notes\xgboost.assets\image-20210922162014992-16322988161305.png)

- approximate algorithm
  - propose candidate splitting points according to **percentiles of feature distribution**
  - **map continuous features into bucket** split by these candidate points
  - aggregate the statistics and find the best solution among **proposals**
  - two variant : when the proposal is given
    - global
    - local -> require fewer candidates
  - extensions:
    - ==directly construct approximate histograms of gradient statistics==?? [22]
    - use binning strategies other than quantile [17]

### Weighted Quantile Sketch

### Sparsity-aware split finding

![image-20210922165728850](D:\笔记\paper_notes\xgboost.assets\image-20210922165728850.png)

# LightGBM

