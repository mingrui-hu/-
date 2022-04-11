## Code

http://lamda.nju.edu.cn/code_gcForest.ashx  

## Inspiration

1. No-theoretical proof:

   - **decision trees and Boosting machines** always work on the **original feature representation** without creating new features   
   - Boosting machines $\rightarrow$ limited model complexity
   - DNN: 3 crucial characteristics: 
     - layer-by-layer processing
     - in-model feature transformation
     - sufficient model complexity

2. From ensemble learning

   - error-ambiguity decomposition

     $ E = \bar{E} - \bar{A}$

     $E$ = the error of an ensemble

     $\bar{E}$ = the average error of individual classifiers

     $\bar{A}$ = the average ***ambiguity*** **(diversity)**

     i.e.  the **more accurate**
     and **more diverse** the individual classifiers, the **better** the ensemble  .

   - (Diverse but not well-accepted) **Diversity measures**

   - Strategy of **==diversity enhancement==**：

     Inject randomness based on heuristics during training.

     a. **Data Sample manipulation**

     - bootstrap sampling $\rightarrow$ Bagging
     - sequential importance sampling $\rightarrow$ AdaBoost

     b. **Input Feature Manipulation**

     - generate different ***feature subspaces*** $\rightarrow$​ the *Random Subspace* approach   : randomly picks
       a subset of features for each individual learner  

     c. **Learning Parameter manipulation**

     - different **parameter settings** $\rightarrow$ different initial weight

     d. **Output Representation manipulation**

     ​	using different output representations to
     generate diverse individual learners  

     - ECOC: error-correcting output code  
     - the Flipping Output method  

     

## gcForest

key: 1. cascade forest structure 2. multi-grained scanning

1. to simulate **deep representation learning** of NN $\rightarrow$ cascade forest structure 

   - Each forest **(base unit)** : two completely random trees + 2 random trees

   - Each layer output: concatenation of class vectors (i.e. #leafs = #classes) from each forest

   - Hyperparameters for each layer: number of forests

   - Automatically determined complexity:

     use validation set to do **k-fold cross validation at each layer**, and expanding to next layer only if current layer does not reach the expected condition. 

     - (me: might be the reason to use class vectors rather than one-hot leaves in each forest?)
     - i.e. sequential layer unfolding

2. feature augmentation $\rightarrow$ multi-grained scanning (sliding window sub-features)

   - expect to create **different feature subspace**?

     - then why use the same set of forests for all 

       sub features?

   - inherited label error for sub-features extracted

     $\rightarrow$ Flipping Output method

   - feature sampling

   - similar composition to skip connection?

     <img src="D:\笔记\paper_notes\DeepForest.assets\image-20210922112139421.png" alt="image-20210922112139421" style="zoom:50%;" />



3. Prediction/Classification ~ similar to max pooling
   - **aggregating** the (#forest) 3-dimensional class vectors at the last level, 
   - and taking the class with the **maximum** aggregated value

**==Q:==** 

1. using ***class vector concatenation as the input vector*** of next level ? isn't error amplified in this way? Error inherited as well?

2. all *sub features （also，highly overlapping as described in the paper）go though the same set of （classification）forests*? does that really make sense，since each instance feature dimension is capturing different aspects, while the splitting procedure are designed for all sub feature procedures?

## Experiments

#### Q:

1. computation resources/computation time comparison?
2. Improvement -gcForest(gbdt) version?

### Related work

1. tree combined with nn-net [29]
2. random-forest [5]
3. completely-random tree forest 
   - iForest [38]
   - sencForest [44] : handling emerging new classes in streaming data  

4. smarter sampling strategies, such as BLB [27], or feature hashing [60]   

5. ***hard negative mining*** strategy may help improve generalization performance  

6. twice-learning strategy [66]  

7. 可能可以支持小样本:

   - The employment of **completely-random tree forests** not only helps enhance diversity, but also provides an opportunity to **exploit unlabeled data**. Note that the growth of completely-random trees does not require labels, whereas label information is only needed for annotating leaf nodes.   

   - Intuitively, for each leaf node it might be able to require only one labeled example if the node is to be annotated according to the majority cluster on the node, or one labeled example per cluster if all clusters in the node are innegligible.
   - This also offers gcForest with the opportunity of incorporating *active learning* [15,25] and/or *semi-supervised learning* strategies [35, 67].  
   - 

