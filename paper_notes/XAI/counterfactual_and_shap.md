### Generating Counterfactual and Contrastive Explanations using SHAP  2019

- 用shap计算全局特征重要性
- 调整重要特征生成counterfactuals
- 没写明白到底给定某一特征f怎么生成的counterfactuals
- 没有任何验证

### Counterfactual Shapley Additive Explanations  

- JP Morgan 2021
- using counterfactual points as the background distribution for SHAPLEY VALUE computation
- Effects of **different background datasets** on the shap value
  - Shapley values explain a prediction of an input **in contrast to** a distribution of background points  
- 3 types of counterfactual methods;
  - Feature Perturbation
  - KNN of different labels (K=10 + euclidean distance)（来自于训练集）
  - Decision Boundary 𝐾-Nearest Neighbours (𝐾-NN∗)  
- 4 public datasets：
  - **GMSC (Give Me Some Credit) [17], HELOC (Home Equity Line Of Credit) [13], LC (Lending Club Loan Data) [18]** and WINE (UCI Wine Quality) [9]  

- ==Q: 使用10个neighborhood不会对shapley marginal的估计准确性造成影响么？==

