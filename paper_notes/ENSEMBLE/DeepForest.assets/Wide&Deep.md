## 

https://chromium.googlesource.com/external/github.com/tensorflow/tensorflow/+/r0.10/tensorflow/g3doc/tutorials/wide_and_deep/index.md

https://branyang.gitbooks.io/tfdocs/content/tutorials/wide_and_deep.html

## The Wide Model: Linear Model with Crossed Feature Columns

-   ==Q: may replace hand-made cross feature with gbdt?==

-   Wide models with crossed feature columns can memorize sparse interactions between features effectively. That being said, one limitation of crossed feature columns is that they do not generalize to feature combinations that have not appeared in the training data. 

## Deep

-   **Each** of the sparse, high-dimensional categorical features are first converted into a low-dimensional and dense real-valued vector, often referred to as an embedding vector. 
-   These low-dimensional dense embedding vectors are **concatenated with the continuous features**, 

-   The embedding values are **initialized randomly,** 
-   and are **trained along** with all other model parameters to minimize the training loss

-   TF code

    ```python
    deep_columns = [
      tf.contrib.layers.embedding_column(workclass, dimension=8),
      tf.contrib.layers.embedding_column(education, dimension=8),
      tf.contrib.layers.embedding_column(marital_status, dimension=8),
      tf.contrib.layers.embedding_column(gender, dimension=8),
      tf.contrib.layers.embedding_column(relationship, dimension=8),
      tf.contrib.layers.embedding_column(race, dimension=8),
      tf.contrib.layers.embedding_column(native_country, dimension=8),
      tf.contrib.layers.embedding_column(occupation, dimension=8),
      age, education_num, capital_gain, capital_loss, hours_per_week]
    ```

-   **Embedding size**:

    Empirically, a more informed decision for the number of dimensions is to start with a value on the order of $klog2⁡(n)$ or$ k\sqrt[4]{n}$, where $n$ is the number of unique features in a feature column and $k$ is a small constant (usually smaller than 10)

-   Con:
    -   However, it is **difficult to learn effective low-dimensional representations** for feature columns when the **underlying interaction matrix between two feature columns is sparse and high-rank**. In such cases, the interaction between most feature pairs should be zero except a few, but dense embeddings will lead to nonzero predictions for all feature pairs, and thus can over-generalize.

### Join Wide & Deep

-   summing up their final output **log odds** as the prediction

    -   for sigmoid:
        $$
        log\_odd = W^TX +B
        $$

-   then feeding the prediction to a logistic loss function

    -   `nn.BCEwithlogits` contains a Sigmoid Layer already

### Training

-   In the experiments, we used **Followthe-regularized-leader (FTRL) algorithm [3] with L1 regularization** as the optimizer for the **wide** part of the model, and **AdaGrad [1]** for the **deep** part

