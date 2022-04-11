# To be explored:

-   Complete random tree vs random tree
    -   Isolation Forest
-   XGBoost
-   LightGBM
-   CatBoost
-   DeepForest
-   Tree-based algo performance on imbalanced datasets?
-   Explanability of tree emsembles?

## XGBOOST

### Summary

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

###  3. Split finding algorithm

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

![image-20210922165728850](./paper_notes/xgboost.assets/image-20210922165728850.png)

## LightGBM

-   aims to : *1. Reduce #data instances* *2. reduce #features* (to deal with sparsity)
-   **GOSS** - Gradient-based One-side sampling
    -   sample ***data instances with larger gradient*** (since there is no sample weight in GBDT) while computing information gain.
    -   **larger gradient $\approx$ under trained** according to **defination of information gain**
-   **EFB** - Excusive Feature Bundling 
    -   claim - **sparse** feature space $\rightarrow$ must features are **exclusive**
    -   reduce **optimal bundling** algorithm to a **graph coloring** problem
        -   Def: features = vertices; edges are added if two features(nodes) are not mutually exclusive
            -   然后找连通子图？UnionFind？
        -    solver: a greedy algorithm with a constant approximation ratio
-   **LightGBM = GBDT with GOSS + EFB**



-   Introduction
    -   GBDT split point finding algorithms
        -   Pre-sorted - enumerating all possible split points on the pre-sorted feature values
            -   $O(\#data * \#features)$
        -   Histogram-based
            -   buckets continues feature values into discrete bins
            -   use bins to construct feature histograms
            -   $O(\#bins * \#features)$

-   Related work
    -   Presorted implementation: Scikit-learn  & gbm in R
    -   Histogram-based: pGBRT
    -   XGBoost: support both presorted + histogram based
-   Concerning Sparse Features
    -   GBDT + Pre-sorted algo: ignorign features with **zero values [13]**??
    -   Histogram-based got no optimzation over sparse features 

### GOSS

-   at each split point(feature $j$, split point $d$), for both left & right side nodes over split point (d)
    -   sample # datasets into 
        1.   Top **a%** large gradient
        2.   sample small graident subset to  size of **(b% * (1- a%))**
    -   add a constant normalizer to the sub-sampled small-gradient datasets $\frac{1-a}{b}$
-   Approximate $V_{j|O}(d)$ on all data instances with $\tilde{V_j(d)}$ on the above sampled datasets
-   **Error analysis (??)**
    -   approximation error
        -   Asymptotic approximation ratio $O(\frac{1}{n_l^j(d)} + \frac{1}{n_r^j(d)} + \frac{1}{\sqrt(n)})$
        -   imbalanced (splitting) dataset -> higher approximation error
    -   generation error

### EFB

-   two issues to consider:
    1.   which features should be bundled together
    2.   how to construct bundle
-   Graph - coloring algorithms 
    -   https://www.whitman.edu/mathematics/cgt_online/book/section05.08.html
    -   Find non-overlapping nodes - adjcent nodes are mutually exclusive in the defined attribute dimnesion (**independent set**)

-   **Issue 1 which features should be bundled together $\rightarrow$ Greedy Bundling** 
    -   1.   construct weighted graph, where $weights = total conflicts btw features $
        2.   Sort the features by degree in graph in descending order
        3.   Assign each feature to an axisting bundle(if bundle conflicts < a threshold K, i.e. the feature and the newly modified bundle are still sparse enough) or create a new bundle(dense feature)
    -   Optimization - more efficient ordering strategy without constructing a real graph
        -   sort by $\#non\_zero \space values$ in each feature (i.e. assume $\#non\_zero \space values \rightarrow higher\space propability\space of\space conflicts  \propto egree(node)$ )
-   **Issue 2 - how to construct bundle - histograms(bins) with offset**

-   Optimation on basic histogram-based algorithms towards zero-valued features

    -   sacrifice memory for (sparse) feature speed up 
    -   use a table to record only non-zero valued entries for each (sparse) features
        -   scan this reduced table when searching for split points and computing information gain $O(\#data) \rightarrow O(\#non-zero \space data)$
    -   does not conflict with basic EFB
        -   can be performed when sparse EFB bundled features still exists

-   ### other materials

    -   [LGBM parameter tuning](https://neptune.ai/blog/lightgbm-parameters-guide)

## CatBoost 2018

### Categorical features

-   low cardinality : one-hot encoding

-   **Target Statistics(Target Mean Encoding)** 

    -   simple TS leads to overfitting
    -   Solver: random permutation  $\rightarrow$ Ordered Target Sequence
        -   inspired by online learning algorithms which expose a temporal sequential order on the input data

-   **Feature Combination**

    -   categorical features' properties: two feature combined to be unique new feature
        -   if convert each feature to numerical feature independently, then newly converted fatures lose this property
            -   Note: LightGBM save this property by EFB on sparse features only
    -   directy consider 2nd order feature combination(both numerical(treated as binary categorical using the split point) and categorical features)

-   Ordered Boosting - **Support Model**

    -   aims to reduce training model gradient bias when  building tree structures 
    -   relaxed models: all $M_i$ shares the same tree structure

-   **Bayesian boosting**

    -   for regularization purpose when choosing split point

    -   param: [`bootstrap_type`](https://catboost.ai/docs/concepts/algorithm-main-stages_bootstrap-options.html)

        

-   One-hot max size

-   Interpretation & XAI

    -   Feature Importance
    -   Feature Interaction
    -   Object Importance

### CatBoost - unbiased - theoritical analysis

#### BG

-   gradient boosting 
    -   Newton method - second order approximation of Loss at step t-1
    -   functional gradient boosting

-   Target statistics
    -   claim to as a common practice in fields such as click-trough rates prediction(such as facebook 2014 paper)
    -   replace the category $x_k^i$ of the $k-th$ training example, with **$one \space numeric$ feature equal to some $target \space statistics$**
        -   estimate the expected target $y$ conditioned by the category $\hat{x_k^i} \approx \mathbb{E}(y | x^i = x_k^i)$
        -   **Q : so WOE encoding is enssentially a type of target statistic(TS) ?** 
        -   AND also has the issue of **conditional shift** since WOE is highly related to the distribution of $p(y | x)$ , and hence require online data & test data to follow a strictly matching distribution as training datasets?
        -   

## Some explanations on CatBoost

-   https://affine.ai/catboost-a-new-game-of-machine-learning/
    -   it gives 1. data preproration suggestions
-   [CatBoost for big data: an interdisciplinary review](https://journalofbigdata.springeropen.com/articles/10.1186/s40537-020-00369-8)

## LightGBM

-   [Understanding LGB parameters](https://neptune.ai/blog/lightgbm-parameters-guide)
-   official [optimization](https://lightgbm.readthedocs.io/en/latest/Features.html) 

## Catboost

-   training parameters:

    https://catboost.ai/en/docs/references/training-parameters/

## Blogs

-   [XGBoost vs. CatBoost vs. LightGBM: How Do They Compare?](https://www.springboard.com/library/machine-learning-engineering/xgboost-random-forest-catboost-lightgbm/)



## 其他相关的树模型

-   2019 Stanford NGBoost
-   
