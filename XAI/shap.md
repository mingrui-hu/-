### Shap 知识点汇总

https://zhuanlan.zhihu.com/p/85791430

#### with lgb booster for binary classification

>   KeyError: 'objective'

https://github.com/slundberg/shap/issues/1042

```python
# solution
booster.params['objective'] = 'binary'
```



==Q:== 

-   Tree Shap ?? why two leaves means no interaction?

https://shap.readthedocs.io/en/latest/example_notebooks/tabular_examples/tree_based_models/Census%20income%20classification%20with%20LightGBM.html

>   ### Train a model with only two leaves per tree and hence no interaction terms between features

>   Forcing the model to **have no interaction terms** means the effect of a feature on the outcome does not depend on the value of any other feature. 
