## 特征选择库

feature-selector

[scikit-feature](https://jundongl.github.io/scikit-feature/)

[结合Scikit-learn介绍几种常用的特征选择方法](https://www.cnblogs.com/hhh5460/p/5186226.html)

### 三种特征选择方式

- 过滤： 相关性/互信息 + 阈值
- 打包(包裹式)：
- 嵌入式: e.g. DT, LASSO, l1正则



## Q

- **PolynomialFeats** vs **Cross Features**?

  ```python
  import sklearn.preproc as preproc
  
  preproc.PolynomialFeatures(degree=2, include_bias=False, interaction_only=False).fir_transform(X)
  ```

  [scikit-learn PolynomialFeatures](https://scikit-learn.org/stable/modules/preprocessing.html#generating-polynomial-features)

- Frequent Itemset & Association Rules & A-Prior algo

### 推荐领域特征交叉方法

- 二阶：FM, FFM
- GBDT(+RF) + LR
- DNN-based

### Wide&Deep

- Wide -> Memorization
  - cross-product transformation: $\phi_k = \Pi_{i=1}^d{x_i^{c_{ki}}}, {c_{ki} \in \{0, 1\}}$
- Deep -> Generalization
- Joint Function: weighted sum of their log odds
- 优化器： wide-part: FTRL with l1 regularization, deep-part: AdaGrad
- 指标: online A/B Test
- 进阶: DCN
- [simple version code](https://zhuanlan.zhihu.com/p/334991736)
- [另一份解析](https://zhuanlan.zhihu.com/p/57247478)

## 自动特征工程

- 主要分为两大类，一类是显式特征组合，‍另一类是隐式特征组合。
  - 显式: RMI[2], CMI[3]
  
    [2] Rómer Rosales, Haibin Cheng, and Eren Manavoglu. 2012. Post-click conversion modeling and analysis for non-guaranteed delivery display advertising. WSDM.
  
    [3] Olivier Chapelle, Eren Manavoglu, and Romer Rosales. 2015. Simple and scalable response prediction for display advertising. TIST.
  
  - 隐式: FM, FFM
  
- 3种策略

  - two-stage: generation-selection strategy

  - rl-based

  - transfer-learning/meta-learning based

    - ExploreKit-learning to rank

    - Learning feature engineering for classification - 2017

      - meta-features do not learn feature relationship (interaction?)
      - better for unary transformation?

      

## AutoCross

- [zh_解读](https://segmentfault.com/a/1190000021328618?utm_source=sf-similar-article)
- numerical features vs categorical cross features
- multi-field cross feature set generation
- workflow:

  - pre-processing -> feature-generation -> feature-set-evaluation
  - preprocessing -> discretization of numerical features
  - preprocessing： multi-granuality discretization（i.e.多个分箱距离形成多个特征， 并且也通过下面的feature-evalution方法进行选择）
  - feature-set-generation: beam search of tree space expanding
  - feature-set-evaluation: field-wise LR + successive halving features(successive mini-batch GD)
- **Infrastructure**

## SAFE

- Operators:
  - Unary: include different discretization methods
  - Binary
  - Terary
  - Group Operators
- Feature-Generation
  - base features$X_i$: narrow-down search space: using XGBoost
  - base features * available operators -> new features $\tilde{X_{i}}$
  - base features + new features -> feature selection stage
- Feature-Selection 
  - input: $\{X_i, \tilde{X_i}\}$
  - information value
  - pearson correlation
  - model-based rankings (tree-model)-> keep features with highest score as base features for the next iteration ($X_{i+1}$)
- Termination: Time/Computation Space

## Comparison of AutoCross & Feature Selection

- Common：Two-Stage Iteration Method
- Difference：
  - Terminating Condition： AC + early stopping
  - Ways to narrow down base features：
    - AC：beam search
    - SAFE：xgboost
  - Operators to generate new features
    - AC: multi-granularity discretization + feature-crossing(product)
    - AC $\subset$ SAFE
  - Feature Selection
    - AC: model-based only
      - narrow-down evaluation space & save compuation resources: successive minibatch GD 
      - evaluation model: field-wise LR
    - SAFE: pipeline
      - narrow-down evaluation space: iv + pearson correlation
      - evaluation model: xgboost



## 参考案例

- [斗鱼风险评分模型建设](https://mp.weixin.qq.com/s?__biz=MzU1NTMyOTI4Mw==&mid=2247547724&idx=1&sn=f233020e841cf168a5652a2243522f73&chksm=fbd78920cca000365a5808010447c13a4eb533669e5100005f637faf59378ee279c6cde2637f&scene=90&subscene=93&sessionid=1629119163&clicktime=1629119194&enterid=1629119194&ascene=56&devicetype=android-29&version=280009a0&nettype=WIFI&abtest_cookie=AAACAA%3D%3D&lang=zh_CN&exportkey=AST0EebSqiJ7C9PjdqGt7Jc%3D&pass_ticket=8iZEmdJUi5PH25pGpHCX8jKz0wOmP93TjRzrBFm9haA21kavCfJoYefEYS9Do%2FXM&wx_header=1):

  - LR -> GBDT +LR -> Wide&Deep(DNN + LR) -> DeepFM(Wide侧改为FM)
  - 后期： 融合更多信息： 序列embedding,  图embedding， 融合序列特征，关系特征

  - base: 单天模型， +加权历史评分 -> 融合模型
  - 团伙评分进行补充， 白评分衡量误杀？
  - 行为序列： 捕捉用户异常行为路径

