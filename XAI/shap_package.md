## 1. Shap 知识点汇总

https://zhuanlan.zhihu.com/p/85791430

https://towardsdatascience.com/interpretable-machine-learning-with-xgboost-9ec80d148d27

-   related notebook: https://slundberg.github.io/shap/notebooks/NHANES%20I%20Survival%20Model.html

-   In comment, questions related to what $f_{x(S)}$ and $E[f(x) | f_{x(S)}]$:

>   Good question. f_x(S) for SHAP values is defined as E[f(x) | x_S]. That means we want the conditional expectation of the model’s output given only a subset of the feature values from the sample x. One way to compute this expectation (that only uses the output of the model trained on all the features) is to **integrate f(x) over the background distribution of feature values not in S**. That integration can be expensive so in Kernel SHAP we approximate it by replacing the features we are not conditioning on with a few background reference values. In Tree SHAP we can do better and estimate E[f(x) | x_S] for a single tree by starting at the root of the tree and then either following one branch if that split feature is in S, or both branches weighted by the number of training samples that went down each branch if the variable is not in S and so we are integrating it out (Algorithm 1 in the Tree SHAP paper).

==Q: why condisioning on a subset  feature values $x(S)$ -> **integrate f(x) over the background distribution of feature values not in S**?==

-   **PDP vs SHAP** : 

    >   Partial dependence plots reflect the expected output of the model if we were to intervene and change exactly one of the model parameters. In contrast, the SHAP value for a feature represents how much that feature impacted the prediction for single sample, **accounting for interaction effects**. So while in general you would expect to see similar shapes in a SHAP dependence plot and a partial dependence plot they will be different if your model has **multi-variable interaction effects** (like AND or OR). **A partial dependence plot has no vertical dispersion** and so no indication of how much interaction effects are driving the model’s predictions.

-   LIME vs SHAP

    >    LIME will produce SHAP values if you replace the heuristic kernels they use with a special Shapley kernel we derived in the NIPS paper. So they are (surprisingly) very related. The key difference is that values from lime are asymptotically “consistent”, **but not “accurate”**, in the sense that they **don’t add up to the current model output.** Note that for this article I used an exact polynomial time tree algorithm, which is greatly preferable to the sample based model agnostic estimation approaches of LIME or Kernel SHAP.

## 2. Shap package error list

#### 1. with lgb booster for binary classification

>   KeyError: 'objective'

https://github.com/slundberg/shap/issues/1042

```python
# solution
booster.params['objective'] = 'binary'
```



#### 2.can only display Explanation objects (or arrays of them)! 

>   ```py
>   AssertionError: visualize() can only display Explanation objects (or arrays of them)!
>   ```

-   官方文档中的

    ```python
    shap.force_plot(explainer.expected_value[1], shap_values[1][0,:], X_display.iloc[0,:])
    ```

    有问题， 应当是 `shap_values.values` ， 其中`type(shap_values) == shap._explanation.Explanation`

    https://stackoverflow.com/questions/66726871/getting-a-mistake-with-shap-plotting

    并且， `shap_values[1][0, :]` -> `shap_values[0, :, 1]`

#### 3. length of features is not equal to the length of shap_values



## 3. SHAP dependence plots

>   show the effect of a single feature across the whole dataset. They plot a **feature’s value vs. the SHAP value of that feature across many samples**. SHAP dependence plots are similar to partial dependence plots, but **account for the interaction effects** present in the features, and are only defined in regions of the input space supported by data. The vertical dispersion of SHAP values at a single feature value is driven by interaction effects, and another feature is chosen for coloring to highlight possible interactions.

>   One the benefits of SHAP dependence plots over traditional partial dependence plots is this ability to distigush between between **models with and without interaction terms**. In other words, SHAP dependence plots give an idea of **the magnitude of the interaction terms** through the **vertical variance** of the scatter plot at a given feature value.

## 4. ==Q:==

-   Tree Shap ?? why two leaves means no interaction?

https://shap.readthedocs.io/en/latest/example_notebooks/tabular_examples/tree_based_models/Census%20income%20classification%20with%20LightGBM.html

>   ### Train a model with only two leaves per tree and hence no interaction terms between features

>   Forcing the model to **have no interaction terms** means the effect of a feature on the outcome does not depend on the value of any other feature. 

-   **shap values** vs **shap interaction values**?

https://shap.readthedocs.io/en/latest/generated/shap.explainers.Tree.html#shap.explainers.Tree.shap_interaction_values

-   Expected values & shap values gives two **negative** values?

    -   negative vs postive effects?

        ```python
        explainer.expected_value[0]
        explainer.expected_value[1]
        
        shap_values[sample_idx, :, 0]
        shap_values[sample_idx, :, 1]
        ```

-   ==!!! TreeExplainer & KernelExplainer gives different base values!==
    -   `path: shap\explainers\_tree.py line865`
-   TreeExplainer, different `feature_perturbation` type depends on whether `data=None` when constructing the `Explainer`

## 5.An introduction to explainable AI with Shapley values

https://shap.readthedocs.io/en/latest/example_notebooks/overviews/An%20introduction%20to%20explainable%20AI%20with%20Shapley%20values.html

-   GAM：General addictive model, all features' contribution(i.e.shap values) sums up to difference between 
    $$
    E[f(x)] - f(x)
    $$

-   one way to train a GAM: 

    -   set XGBOOST with  depth = 1 -> ==? because of the gradient boosting nature?==

-   Interaction effects

    -   model NOT addictive in the probability space.

-   **Q:** 

    -   addictive natures -> sum up over all input features of a single sample

    -   ==is it meaningful if sum up a single input feature's shap over all samples?== --> feature shap **barplot**

    -   dealing correlated features? ->feature redundancy clustering -> **clustering over what?** -> original feats or shap values?

        https://shap.readthedocs.io/en/latest/example_notebooks/overviews/Be%20careful%20when%20interpreting%20predictive%20models%20in%20search%20of%20causal%C2%A0insights.html

    -    

-   Max value over feature ships --> can indicates **infrequent but high magnitude** effects!

## 6. Understanding Tree SHAP for Simple Models[(link)](https://shap.readthedocs.io/en/latest/example_notebooks/tabular_examples/tree_based_models/Understanding Tree SHAP for Simple Models.html#Understanding-Tree-SHAP-for-Simple-Models)

>   The SHAP value for a feature is the average change in model output by conditioning on that feature when introducing features one at a time over all feature orderings. 

-   considering effects btw shap values & feature interactions in tree -- ==Q: relation?==
    -   two feature AND
    -   two feature OR
    -   two feature XOR
    -   two feature AND + boost
-   ==Q: difference: tree-based feature importance vs treeSHAP?==

## 7. python version of TreeSHAP implementation

https://shap.readthedocs.io/en/latest/example_notebooks/tabular_examples/tree_based_models/Python%20Version%20of%20Tree%20SHAP.html#Python-TreeExplainer

### 8. Causal vs Prediction task

-   unobserved confounding problem
-   observed confounding problem
    -   related to feature redundancy
-   **Causal Inference Packages**
    -   econML
    -   CausalML
-   Detect true causal effects
    1.   observed upstream con-founders -> **DOUBLE ML**:(causal features & control features)
    2.   downstream consequences -> drop the downstream features -> to estimate full causal effects rather than only direct effects

#### Visualization

https://medium.com/dataman-in-ai/the-shap-with-more-elegant-charts-bc3e73fa1c0c

-   global interpretability: (a) Bar plot, (b) Cohort plot, and (c) Heatmap plot.
-   local interpretability: (d) Waterfall plot, (e) Bar plot, (f) Force plot, and (g) Decision plot

### Shap interaction value

-   https://www.kaggle.com/wrosinski/shap-feature-importance-with-feature-engineering

## Shap Explainers

-   Tree-based algos -> `TreeExplainer`
-   DeepNN -> `DeepExplainer`
-   Others -> `KernelExplainer`
-   https://towardsdatascience.com/explain-your-model-with-the-shap-values-bc36aac4de3d
