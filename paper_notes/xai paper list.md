1. On the opportunities and risks of foundation models
2. Wide&Deep
3. DeepCross
4. DIN
5. DeepFM
6. DeepAR
7. TCN
8. Model Ensemble for Click Prediction in Bing Search Ads - 2017
9. Practical Lessons from Predicting Clicks on Ads at Facebook - 2017



## XAI



-   SHAP： [A Unified Approach to Interpreting Model Predictions](https://arxiv.org/abs/1705.07874)
-   Sumedha Singla, Brian Pollack, Junxiang Chen, and Kayhan Batmanghelich. Explanation by progressive exaggeration. arXiv preprint arXiv:1911.00483, 2019  

### Tree methods

-   Q. Zhang, Y. Yang, H. Ma, and Y. N. Wu, “Interpreting CNNs via decision trees,” in Proc. IEEE Conf. Comput. Vis. Pattern Recognit., 2019, pp. 6261–6270.  

### Shapley related:

- The Explanation Game: Explaining Machine Learning Models Using Shapley Values  2020
- David S. Watson. 2021. Rational Shapley Values.   -- A Baysian method

### Counterfactual related

- Reasoning: The Hidden Assumptions Behind Counterfactual Explanations and Principal Reasons  2019
- Arnaud Van Looveren and Janis Klaise. Interpretable counterfactual explanations **guided by prototypes**, 2019.  

#### Generative

- **GAN**: S. Liu, B. Kailkhura, D. Loveland, and Y. Han. Generative counterfactual introspection for explainable deep learning. In 2019 IEEE Global Conference on Signal and Information Processing (GlobalSIP), pages 1–5, 2019.  
- **VAE**: Shalmali Joshi, Oluwasanmi Koyejo, Warut Vijitbenjaronk,
  Been Kim, and Joydeep Ghosh. Towards realistic individual recourse and actionable explanations in black-box decision making systems. CoRR, abs/1907.09615, 2019.  

### Unify feature attribution & counterfactual

- Towards Unifying Feature Attribution and Counterfactual Explanations: Different Means
  to the Same End  2021
- CERTIFAI: A Common Framework to Provide Explanations and Analyse the Fairness and
  Robustness of Black-box Models.  2020
  - Applies counterfactuals to examine robustness, interpretability, transparency, and fairness.  
  
- Matt Chapman-Rounds, Umang Bhatt, Erik Pazos, Marc-Andre Schulz, and Konstantinos Georgatzis. 2021. FIMAP: Feature Importance by Minimal Adversarial Perturbation.  
- **Tree-based**: Riccardo Guidotti, Anna Monreale, Salvatore Ruggieri, Dino Pedreschi, Franco
  Turini, and Fosca Giannotti. 2018. Local Rule-Based Explanations of Black Box
  Decision Systems. http://arxiv.org/abs/1805.10820  

### Feature attribution guided counterfactual generation

- Carlos Fernández-Loría, Foster Provost, and Xintian Han. 2021. Explaining DataDriven Decisions Explaining Data-Driven Decisions made by AI Systems: The Counterfactual Approach. arXiv:2001.07417  
- Yanou Ramon, David Martens, Foster Provost, and Theodoros Evgeniou. 2020. A
  comparison of instance-level counterfactual explanation algorithms for behavioral and textual data: SEDC, LIME-C and SHAP-C. Adv. in Data Analysis and
  Classification 14 (2020), 801–819.  

### Prototypes & Cristisism

- Jacob Bien and Robert Tibshirani. Prototype selection for interpretable classification. The Annals
  of Applied Statistics, pages 2403–2424, 2011  

- Been Kim, Rajiv Khanna, and Oluwasanmi O Koyejo. Examples are not enough, learn to criticize!
  criticism for interpretability. In Advances in Neural Information Processing Systems, pages 2280–
  2288, 2016.  

### Incorporating causal structures

- Divyat Mahajan, Chenhao Tan, and Amit Sharma. 2020. Preserving Causal Constraints in Counterfactual Explanations for Machine Learning Classifiers.
  http://arxiv.org/abs/1912.03277  

## Counterfactual

- ~~Counterfactual Explanations for Machine Learning on Multivariate Time Series Data~~

  https://arxiv.org/pdf/2008.10781.pdf

- Causal inference for time series analysis: problems, methods and evaluation

  - https://link.springer.com/content/pdf/10.1007/s10115-021-01621-0.pdf

- ~~Shubham Rathi. 2019. Generating Counterfactual and Contrastive Explanations using SHAP. In 2nd Workshop on Humanizing AI (HAI) at IJCAI ’19. arXiv:1906.09293~~  

  - https://arxiv.org/pdf/1906.09293.pdf

- CX-ToM: Counterfactual Explanations with Theory-of-Mind for Enhancing Human Trust in Image Recognition Models

- ~~Counterfactual Shapley Additive Explanations~~

- ~~Conditional Generative Models for Counterfactual Explanations~~

- NIPS2017 reliable-decision-support-using-counterfactual-models

- COUNTERFACTUAL EXPLANATIONS WITHOUT OPENING THE BLACK BOX

- ~~A Survey of Contrastive and Counterfactual Explanation Generation Methods for XAI~~

- WWW22 Learning and Evaluating Graph Neural Network Explanations based on Counterfactual and Factual Reasoning

  - https://mp.weixin.qq.com/s/-Dv0bPjup6kyFSzrPrfU0w

- AAAI 2019 FACE: Feasible and Actionable Counterfactual Explanations

- Adam White and Artur d’Avila Garcez. 2019. Measurable Counterfactual Local Explanations for Any Classifier. http://arxiv.org/abs/1908.03020  

- S. Liu, B. Kailkhura, D. Loveland, and Y. Han, ‘‘Generative counterfactual introspection for explainable deep learning,’’ in Proc. IEEE Global Conf. Signal Inf. Process. (GlobalSIP), Nov. 2019, pp. 1–5.  

#### gradient based counterfactual?

- Mark T. Keane and Barry Smyth. 2020. Good Counterfactuals and Where to Find Them: A Case-Based Technique for Generating Counterfactuals for Explainable AI (XAI). arXiv:cs.AI/2005.13997  

#### Finance counterfactual

- 2018 Interpretable Credit Application Predictions With Counterfactual Explanations  
- P. Bracke, A. Datta, C. Jung, and S. Shayak, “Machine learning explainability in finance: An application to default risk analysis,” Staff Working Paper No. 816, Bank of England, 2019.  
- C. Chen, K. Lin, C. Rudin, Y. Shaposhnik, S. Wang, and T. Wang, “An interpretable model with globally consistent explanations for credit risk,” 2018, arXiv: 1811.12615.  

#### Batch of counterfactuals at once

- Susanne Dandl, Christoph Molnar, Martin Binder, and Bernd Bischl. 2020. MultiObjective Counterfactual Explanations. http://arxiv.org/abs/2004.11165  
- Ramaravind K. Mothilal, Amit Sharma, and Chenhao Tan. 2020. Explaining
  Machine Learning Classifiers through Diverse Counterfactual Explanations.
  In Proceedings of the Conference on Fairness, Accountability, and Transparency
  (FAccT) (FAT* ’20). Association for Computing Machinery, New York, NY, USA.
  https://doi.org/10.1145/3351095.3372850  
- Kentaro Kanamori, Takuya Takagi, Ken Kobayashi, and Hiroki Arimura. 2020.
  DACE: Distribution-Aware Counterfactual Explanation by Mixed-Integer Linear
  Optimization. In International Joint Conference on Artificial Intelligence (IJCAI),
  Christian Bessiere (Ed.). International Joint Conferences on Artificial Intelligence
  Organization, California, USA, 2855–2862. https://doi.org/10.24963/ijcai.2020/
  395  

#### Generative 

- Martin Pawelczyk, Johannes Haug, Klaus Broelemann, and Gjergji Kasneci.
  \2020. Learning Model-Agnostic Counterfactual Explanations for Tabular Data. ,
  3126–3132 pages. https://doi.org/10.1145/3366423.3380087 arXiv: 1910.09398.  
- conditional subspace VAE: Michael Downs, Jonathan Chu, Yaniv Yacoby, Finale Doshi-Velez, and Weiwei. Pan. 2020.       CRUDS: Counterfactual Recourse Using Disen tangled Subspaces. In Workshop on Human Interpretability in Machine  Learning (WHI). https://finale.seas.harvard.edu/files/finale/files/cruds-_counterfactual_recourse_using_disentangled_subspaces.pdf
- Sumedha Singla, Brian Pollack, Junxiang Chen, and Kayhan Batmanghelich. Explanation by progressive exaggeration. arXiv preprint arXiv:1911.00483, 2019.  
- Lore Goetschalckx, Alex Andonian, Aude Oliva, and Phillip Isola. **GANalyze**: Toward visual definitions of cognitive image properties. In Proceedings of the IEEE/CVF International Conference on Computer Vision, pages 5744–5753, 2019  
- Sumedha Singla, Brian Pollack, Stephen Wallace, and Kayhan Batmanghelich. Explaining the black-box smoothly-a counterfactual approach. arXiv preprint arXiv:2101.04230, \2021.  
- Javier Antoran, Umang Bhatt, Tameem Adel, Adrian Weller, and Jose Miguel Hern ´ andez-Lobato. Getting a clue: A method for explaining uncertainty estimates. arXiv preprint arXiv:2006.06848, 2020  
- **Deep Representation**: Assaf Shocher, Yossi Gandelsman, Inbar Mosseri, Michal Yarom, Michal Irani, William T Freeman, and Tali Dekel. Semantic pyramid for image generation. In Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition, pages 7457–7466, 2020.  

### Discussion

- Thibault Laugel, Marie-Jeanne Lesot, Christophe Marsala, and Marcin Detyniecki. 2019. Issues with post-hoc counterfactual explanations: a discussion. arXiv:1906.04774  
- Solon Barocas, Andrew D. Selbst, and Manish Raghavan. 2020. The Hidden
  Assumptions behind Counterfactual Explanations and Principal Reasons. In Proceedings of the Conference on Fairness, Accountability, and Transparency (FAccT)
  (FAT* ’20). Association for Computing Machinery, New York, NY, USA, 80–89.
  https://doi.org/10.1145/3351095.3372830  
- Kacper Sokol and Peter Flach. 2019. Desiderata for Interpretability: Explaining
  Decision Tree Predictions with Counterfactuals. Conference on Artificial Intelligence (AAAI) 33 (July 2019). https://doi.org/10.1609/aaai.v33i01.330110035  
- Thibault Laugel, Marie-Jeanne Lesot, Christophe Marsala, Xavier Renard, and
  Marcin Detyniecki. 2019. The Dangers of Post-hoc Interpretability: Unjustified
  Counterfactual Explanations. http://arxiv.org/abs/1907.09294  
- André Artelt and Barbara Hammer. 2019. On the computation of counterfactual
  explanations – A survey. http://arxiv.org/abs/1911.07749  

### Tools

J. Wexler, M. Pushkarna, T. Bolukbasi, M. Wattenberg, F. Viégas, and J. Wilson.
\2020. The What-If Tool: Interactive Probing of Machine Learning Models. IEEE
Transactions on Visualization and Computer Graphics 26, 1 (2020), 56–65  


## Contrastive

- Explanations based on the Missing: Towards Contrastive Explanations with Pertinent Negatives
  - https://github.com/IBM/Contrastive-Explanation-Method
- Thai Le, Suhang Wang, and Dongwon Lee. 2019. GRACE: Generating Concise and Informative Contrastive Sample to Explain Neural Network Model’s Prediction. arXiv:cs.LG/1911.02042  
- J. Labaien, E. Zugasti, and X. D. Carlos, ‘‘**Contrastive explanations for**
  **a deep learning model on time-series data**,’’ in Big Data Analytics and
  Knowledge Discovery (Lecture Notes in Computer Science), vol. 12393.
  Berlin, Germany: Springer, 2020, pp. 235–244 

## 因果

- 清华崔鹏等Nature子刊最新论文：稳定学习建立因果推理和机器学习的共识基础
