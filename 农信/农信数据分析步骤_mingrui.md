- 现有数据情况:

  - 循环贷

  - 账户转出, 转入信息 

    四个ID标记:客户ID、贷款合同号 + 贷款账号 + 机构号

    基于贷款账号进行标记， 目前没有用到行社信息

- 目标:

1. 查看数据

2. 明确问题(输入，输出，损失函数)，形式化建模

3. 现有模型和report， 复现

4. 现有数据：

   ​	a. 字段类别

   ​	b. 总数据量， 数据缺失情况以及重复率

   ​	c. 字段的最大最小，quatile分布，      空值， unique value情况

   ​	d. 按 正负样本 分别统计

   ​		i. 如果没有标签， 将step m提前

   ​		ii. 正负样本比例

   ​		iii. 各字段分布情况

   ​	e. quantile 分布， 空值， 极值，       方差等

   ​	f. record时间分布，记录时间间隔(可能需要按客户id， 贷款账号统计) 是否等值分布

   ​	g. toad eda分析

   ​	h. toad 字段简单信息: iv， 基尼值等

   ​	i. 按几个可能的主要字段(例如客户id，      贷款机构id)聚类分析

   ​	j. 简单降维分析及可视化

   ​	k. 按照多个客户id， 尝试采样并查看e.g账户转出, 转入信息

   ​	l. 相关性、共线性分析，卡方检验等， 尝试关联分析 

   ​	m. 账龄及滚动率分析

5. 基于客户画像的挖掘:

   1. 人的画像： 年纪，地域，年龄段，毕业院校，工作年限，住房情况等
   2. 按照画像分用户全体， 再进行特征相关性、重要性分析
   3. 考虑： 人的分类 + 金融特征

6. 数据集分割: train, val, oot

7. DT/RF进行简单特征筛选作为特征工程的base

8. 如果没有可用, 用单独的GBDT 及 LR分别建立baseline1， 2

**Q**：预测变量(信用评级？授信额度(定价模型)？授信利率(定额模型)？)？反馈机制？

## Ref

- [link1](https://eason.blog.csdn.net/article/details/84376197?utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7Edefault-15.control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7Edefault-15.control)
- [link2](https://blog.csdn.net/weixin_41712808/article/details/85700002)

