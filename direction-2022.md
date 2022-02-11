### 时序

- 时序可解释性 -> extends to causal ML

    - multi-level interpretation requests

        - Local:
            - 行为序列pattern - 时间子序列
            - feature attribution
            - 通常需要: 有意义的物理特征
        - Global:
            - 每一类的共性序列特征
            - 见到的方法: filter clustering (CNN-based)

    - 不同的方法：

        - feature attribution， gradient-based saliency map， model-agnostic(e.g. generative model, inverse optmization)，**counterfactual**,  wavelet decomposition

    - 多标签场景

        

- 时序预测 -> extends to 多模态

    - 路径很多，**怎么选**, **怎么对比**
        - Deep Baysian: / Gaussian Process
        - 控制： Deep State Space Model - Kalman Filter, etc.
        - 信号处理: 时域方法 vs 时频域方法
        - STL分解、 correlation类， (e.g.ARIMA） 
        - 序列模型:  HMM -> TCN, etc.
    - 关系： CNN-based models/FFT-小波分解-learnable models/(动态学习的)shapelets(- similar to inception module in CV) ? 
        - 是否存在共性？
    - 怎样结合多时间/采样粒度数据
    - 多源数据融合
        - 怎样融合静态数据? 
        - 外界宏观指标对时序数据的影响？
        - 多模态数据融合， e.g. + KG？
    - Noise-robustness
        - 如何对声称noise-robust的模型进行测试？ i.e.如何设计对抗样本？
    - 子序列不重叠？
    - 子序列存在叠加态？

- 时序生成模型 -> extends to 小样本/**Few-shot**

    - 背景： 
        - 工业数据集量小且无标注或只有几个标注，但可能有大量无标注数据， 同类问题的数据集间差距较大
    - ~仿真

- 时空网络 -> extends to 动态图网络/ST-graph

    - 场景： 每个样本并不是i.i.d的， e.g.量化
    - spatial-temporal graph？
        - 如何定义边 ？ 相似度？
    - 图的演变过程 - nodes & edges？

- 先验 - combined with: 知识图谱



### Ref:

- 微信专项 3.3. 长序列建模研究
  随着用户在直播上观看行为越来越丰富，用户item序列也不断在增长。如果能从**长序列**中更好地学习用户的兴趣，那自然能提升产品的用户粘性，从而提高DAU和人均观看时长。金融借贷领域中，逾期情况层出不穷，如果能更好地处理用户历史行为序列，从**行为序列**中发现问题，就能进一步降低逾期率，从而带来更多的收益。使用序列特征进行attention处理在推荐系统，金融，自然领域处理等领域特别重要，**序列过长**时，sum pooling，mean pooling，attention目前都不能取得很好的效果，同时，很多序列处理的方法复杂度会随着序列长度成平方的增长，解决好长序列建模的问题可以优化效果和性能。
  科研目标：实现相关算法在实际的金融风控和推荐业务落地，金融风控方面主要通过提升模型auc，在保证拦截用户相同的情况下，欺诈比例下降3%；在推荐业务方面通过提升模型auc，应用到业务中提升业务的转化率提升3%。形成一套**挖掘长序列建模的方案技术方案**，产出高水平论文2篇。
  关键词：金融反诈骗，推荐系统，自然语言处理。
- 蚂蚁知识图谱算法工程师 - OD
  1.   知识图谱建设， 基于内外部**多源数据**， 通过知识抽取、知识融合、知识推理等算法能力， 构建网商银行超大规模知识图谱， 为各大业务场景提供算法能力支持
  2.   知识图谱算法创新与应用， 包括但不限于： 自然语言处理、图学习、图神经网络等算法， 打造可迭代、高质量的**图谱推理算法底盘**， 在**企业金融、营销推荐、风控**等场景创造业务价值
  3.   要求：
       1.   在**图学习、图神经网络**等领域有丰富的算法研究经验，对包括**迁移学习、增强学习、在线学习**等具有一定的理解和认识
       2.   能将微贷信用等金融场景抽象为算法问题

### suggestion

-   mode1: + 一个方向切入， 场景支撑
-   mode2: 癫痫检测 - 解决一个场景
-   domain adaption
    -   domain generalisation

-   可解释性
-   Few-Shot 
    -   多种方法相关
    -   pre-training 
-   评价问题的价值
    -   e.g. 细化场景，有价值的点
    -   e.g. 用电量- 衡量经济复苏能力的差异性
-     场景出发-better

-   从一个场景出发， 泛化到其他适用场景