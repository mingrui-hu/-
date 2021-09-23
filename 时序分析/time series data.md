## 我自己的总结

- Forecasting textbook

- [时序收集](https://github.com/youngdou/awesome-time-series-analysis)



- [WSDM 2021 | 时间序列转化为动态图进行表示](https://zhuanlan.zhihu.com/p/357324652)
- [上面的专栏](https://www.zhihu.com/column/c_1311621896840736768)
- 传统统计分析
  - https://zhuanlan.zhihu.com/p/296284345
  - [有statsmodel代码](https://zhuanlan.zhihu.com/p/77063373)
  - [for finance](https://zhuanlan.zhihu.com/p/36123737)
  - [another one](https://zhuanlan.zhihu.com/p/33775830)
  - ARIMA
    - [ppt](https://zhuanlan.zhihu.com/p/32584136)
    - [a post](https://zhuanlan.zhihu.com/p/145876917)
- DeepAR
  - [机器之心解读](https://baijiahao.baidu.com/s?id=1669194920959781050&wfr=spider&for=pc)
- DTW
- Kalman Filter
- Informer
- TCN-based

- Time2Graph
- [SLS](https://www.zhihu.com/zvideo/1313476410884235264)
  - [阿里云官方](https://help.aliyun.com/document_detail/172129.html?spm=a2c4g.11186623.6.1128.23d0659d0vQCXO)
- tsfresh & TSFEL
- Facebook-Prophet

- 时序图

### References from [post](https://zhuanlan.zhihu.com/p/264584565)

1. **[analytics : Time-series forecast](https://link.zhihu.com/?target=https%3A//www.analyticsvidhya.com/blog/2018/02/time-series-forecasting-methods/)**；
2. **[知乎 arima详解](https://zhuanlan.zhihu.com/p/49746642)**；
3. **[Forecasting at Scale Facebook](https://link.zhihu.com/?target=https%3A//peerj.com/preprints/3190.pdf)**；
4. **[Wiki Arima](https://link.zhihu.com/?target=https%3A//zh.wikipedia.org/zh-cn/ARIMA%E6%A8%A1%E5%9E%8B)**;
5. **[ARIMA模型详解](https://link.zhihu.com/?target=https%3A//danzhuibing.github.io/ml_arima_basic.html)**;
6. **[Fbprophet 使用官网](https://link.zhihu.com/?target=https%3A//facebook.github.io/prophet/docs/installation.html%23python)**;



- [一篇不知道好不好的综述](https://zhuanlan.zhihu.com/p/385138525)



## 案例

[收集](https://zhuanlan.zhihu.com/p/85109460)

[金融时序分析](https://zhuanlan.zhihu.com/p/38320827)



- Q:

ACF vs 偏自相关PACF？





# 别人的总结



- datawhale[总结](https://blog.csdn.net/Datawhale/article/details/114683753?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_title~default-1.control&spm=1001.2101.3001.4242)
  - Gramian Angular Field (格拉姆角场GAF)
  - Short Time Fourier Transform (短时傅里叶变换)
  - TCN
  - 需要注意:
    - 时间卷积网络的含义，dilated-convolution 和 causal-convolution
    - prophet预测原理，各参数对模型拟合效果、泛化效果的影响



- [csdn](https://blog.csdn.net/qq_34919792/article/details/104262255)
  - dtw + knn
- [另一个](https://towardsdatascience.com/a-brief-introduction-to-time-series-classification-algorithms-7b4284d31b97)
  - csdn[翻译](https://blog.csdn.net/weixin_26716079/article/details/108971614?utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.control&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.control)

## Python 库收集

https://github.com/MaxBenChrist/awesome_time_series_in_python

## Prophet

- Decomposable model
- Model Fitting Page 13 section3.4
  - MAP estimate 
  - Stan L-BFGS
- Hyperparam/Components to tune:
  - Capacities -> total market size
  - Changepoints
  - Holidays and Seasonality
  - Smoothing parameters 
    - for trends & seasonality





## Pytorch-forecasting

- inteprete output
  - partial dependency plot?
  - variable importance?



## [GLUONS](https://ts.gluon.ai)

- [aws blog](https://aws.amazon.com/cn/blogs/china/gluon-time-series-open-source-time-series-modeling-toolkit/?nc1=b_rp)

## TSLEARN

- time series shapelets
- [a post](https://zhuanlan.zhihu.com/p/358648965)



## [pyts](https://pyts.readthedocs.io/en/stable/)



## paper list

1. Temporal Fusion Transformer

- multi-horizon?
- interpretable?
- time importance measures?

2. N-beats
   - interpretable forecasting??

