### 

-   1.   本质就是1dim的 Inception Module
    2.   强行adverserial 的套概念 + 没有generator用discriminator强行定义了一个伪generator goal -> 有问题
    3.   本质是一个multitask training 
    4.   关于interpretability的强行解释 -> 非常贴近单个real sample 的 shapelets 只能说明overfit，除非对特定samples进行clustering然后比较，但是它！没！有！
    5.   只考量了univariate -> 强行解释 `for fair comparison` 不与自己的基线比较multivariate -> 为什么不能自己实现一次baseline呢？
    6.   结果: 85 个数据集只有3个accuracy强于baseline， 并且又一次强行模糊解释