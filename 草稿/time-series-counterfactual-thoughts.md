**目前的问题**

1. 目前找到了粗略的研究问题， 没有想到一个很好的设计方案，是应该继续阅读文献(比如去找一下生成模型/GAN相关的文献), 先设计好自己的方法； 还是先复现实验下现在参考的文献，从中优化现有的问题和方案呢？

2. 怎么确定现在找到的这些研究问题**是不是有价值**？

   - 因为采取从方法到场景的方式，还没有找到合适的场景创新点，似乎无法从场景出发评价它的价值？

   - 或者又太宏大(按照我的能力)很难实现？怎样评估可能需要的时间呢？

   - 或者很多想法是不是*熟悉这个领域的人*会很容易想到？所以应该继续搜文献?

3. 从方法到场景，怎样给这个方法**找到合适的数据集和场景**？ 

   - 直接沿用参考文献的? 比如, 结构化数据的贷款申请？

   - 因为从场景到方法、自底向下的方式可能做不到，受限于场景数据和算力暂时无法打通

4. 怎样把握进度呢？该花多久去阅读文献，多久去复现，或者多久去做自己的实验呢？
   - 或者，花一个多月看文献是不是太久？

## Summary

1. 计算效率问题： 
   - SHAP生成datasets较慢且缺少特征交互
2. 基础的单一反事实样例并没有针对每个特征/时间窗给出量化的结果， 到底是哪种特征(哪个时间段发生了什么样的变化)导致了结果P？这样就没法计算比较两个实例的差异
3. 冲突问题：
   - 如果同时部署几个可解释方法，例如feature attribution & saliency map & feature attribution， 如果发生冲突，该信任哪一个？
4. 时间序列问题：
   - 考虑多一层时间维度的变化

## 现有研究的基础

1. 使用条件生成模型去批量生成解释

2. 可解释与Feature Attribution的结合
   1. 使用Feature Attribution指导反事实样本生成时的特征选择
   2. 使用反事实方法(KNN) 生成 SHAP的背景集(虽然目的不是为了解决计算效率)
   3. 统一二者的
3. 多元时间序列的反事实，目前直接随机替换掉一个特征的整个序列
4. 多元时间序列使用RCGAN生成反事实解释
5. 将目标分类器 融入GAN的优化过程中

## 想到的解决方法

- 2个大角度
- 使用一个生成模型 -> 同时生成反事实解释和shap？可能的话在通过设计(代理)的生成模型的结构， 输出 shapelets/saliency map? 进行互相验证？
- 扩展至时间序列上的时间维度？

## 细节们

### 1. A uniform model?

- Try to find a (or more?) model that can answer the following 5 questions for each individual sample (locally) efficiently  (ranked by priority from my understanding):

  1. **Why P (not Q)?**
     - 1.1 This question try to find the exact reason why the sample $x$ is classified to a class $P$ rather than $Q$. 
     
     - 1.2 Its important to **quantify** it and have a **reference point**. This comes from the fact that， given an independent  feature attribution vector $v_i$ for sample $x_i$, people have no sense how far the feature attribution number is away from the boundary(i.e the scale of the number is important), hence of no use to help making decisions. 
       - in order to compare, we want this method to satisfy **additivity & symmetry**.
         - Currently two methods satisfy the requirements: IG & SHAP
       - that say, some thoughts give to **combine Prototypes with Feature attribution** methods?
       - For **choosing reference points**:
         - consider how Integrated Gradients & DeepLift do？
         - prototypes & criticisms
         - 反向优化？maximum activation map on the target node?
     
  2. **How much** (away from the decision boundary to the expected class)? [for classification & anomaly detection]?
     - Since a flipped class may be expected, it involves to answer the question, by adjusting which features and by what extent will be able to adjust the probability to  the **decision boundary**, say e.g. $P=0.5$ for binary classification
     - Thoughts: 
       - same as in 1.2 , may also compare with **prototypes** , but at the level of feature value itself.
       - Similar to ROC curve, may sample a counterfactual for each probability threshold?
     
  3. **What if** (How to improve) ?
     - This is basically a question that counterfactual itself can tackle.
     - **Efficiency:** may focus on how to generate multiple counterfactuals for a single/multiple inputs at one inference time.
     
  4. How much should we trust the results & the explanations?
  
     - How to utilize **Uncertainty** Map?
     - How to ensure the generated (either realistic/synthetic) counterfactual explanations are truly a counterfactual rather than an **adversarial** samples, or in other words, an  **misclassification** caused  by model overfitting?
     - May evaluate uncertainty on both input & explanation? 
       - what to do with **highly confident misclassification**? -> may manually refer back to 1, check the feature attribution?
  
  5. **Feasibility & Actionability**:
     - Most research solve this by adding explicit constraints on mutable and immutable features
     - Explicitly choose feature sets might ignore the feature-wise interaction
     - For time series, we also need to consider which section on the time axis to be sythethesised
     - for certain application, e.g. loan application
     - Thoughts: conditional generative model
       - using templates? masking？
       - 对比学习？
       - masking
       - 时序补全/时空补全？
       - 允许专家根据经验指定counterfactual产生的特征维度， 并通过交互工具允许专家介入或打标修正？并更新explainer & classifier？
  
- The questions above is intended to answer in **one uniform model**. Current research mostly focus on one individual question or a uniform of two(feature attribution&counterfactual). Motivation for a uniform framework comes at two points:

  1. Some of the questions may be solved on **a common base**. 
     1.  Q1 & Q2 may have **common reference points** generated from the same module. 
     2. Q1 & Q2 可以从multiple counterfactuals & background datasets结合？公用一个生成模型？
  2. Questions are mutually supported and **complementary**. Isolated questions are of no use to help make decisions or improve users' systems. (==Scenario Examples==). Some explanation methods are not quantified, some are not intuitive for certain types of data(especially time series & image), but a combination of both may be promising.
  3. We could though, deploy 4 independent explainers, each aims to answer one question, e.g. one for feature attribution, one for counterfactual, one for uncertainty. However, **computation efficiency** will be a big issue. Imagine the size of your explanation system is several times of your original model. Also, we then need 4 evaluations system to evaluate the quality of each explainer. If explanation **conflicts** occur, we would face the same condition as encountered by multi-data source fusion in self-driving: which explanation(source) is correct, since they comes from completely different models?
  4. The explanations will be mutually evaluated. E.g. if a counterfactual is of no sense, human experts might find some clue through feature attribution and uncertainty level.  

- Better: if we could design the framework so that its **both global &local**?

### 2. Other considerations/Limitations

1. Different application scenarios might find different types of explanations more interpretable and useful. (e.g. saliency map vs shap)
2. Small models, e.g. Decision Tree/ Tree Ensembles mostly are chosen due to a **limition of computation resource**, in that case, we definitely would not expect the explanation system to be a huge monster.
3. Extension to **time series**, finer **timing granularity**
   - contribution/saliency over time axis (continuous time window or discrete time step)
4. For time series & temporal-spatio graph, consider connection to **signal processing**?
   - Fourier Operator?
   - Fourier/Wavelet Network?
   - Filter activation map?
5. Categorical features
6. Ignored Issues by now:
   - Ignore causal structure discovery

### 3. Evaluation

1. Is the explainer **robust**? -> **Adversarial** samples

   - for a pair of inputs: a clean, precise input & a noisy version, do they have similar explanations (either feature attributions or examples)? 

   - This may also help answer the question 4, in the aspect of adversarial samples.

2. 是否可能结合信息论进行测量？

   - 最新两篇：
     - 交大 
     - NYU phd thesis

3. How to evaluate **fairness** of the models?

4. 不同解释方法间相互验证？

   - Designing white-box classifier for evaluation purpose?
   - e.g. 使用NN - 与显著图比较

5. 使用简单LR进行验证

### 4. Extension to multi-modality models

