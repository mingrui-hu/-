#### multiple input channel & multiple output channel

https://d2l.ai/chapter_convolutional-neural-networks/channels.html

-   **multiple input (one output channel)**：

    However, when \($c_i>1$\), we need a kernel that contains a tensor of shape \($k_h\times k_w$) for *every* input channel. Concatenating these \($c_i$\) tensors together yields **a convolution kernel of shape** \($c_i\times k_h\times k_w$\). Since the input and convolution kernel each have \($c_i$\) channels, we can perform **a cross-correlation** operation on the two-dimensional tensor of the input and the two-dimensional tensor of the convolution kernel **for each channel**, **adding the \($c_i$\) results together (summing over the channels) to yield a two-dimensional tensor**. This is the result of a two-dimensional cross-correlation between a multi-channel input and a multi-input-channel convolution kernel.

-   **multiple output**：

    Denote by \($c_i$\) and \($c_o$\) the number of input and output channels, respectively, and let \($k_h$\) and \($k_w$\) be the height and width of the kernel. To get an output with multiple channels, we can create a kernel tensor of shape \($c_i\times k_h\times k_w$\) for *every* output channel.

    We concatenate them on the output channel dimension, so that **the shape of the convolution kernel** is \($c_o\times c_i\times k_h\times k_w$\)

    -   final output size: $b\times c_o \times$ output_feature_map_size

### 1*1 convolution

-   effectively equals to a FCN with weights of size $c_i * c_o$, which is shared across every elements(pixels)

    >   [Fig. 6.4.2](https://d2l.ai/chapter_convolutional-neural-networks/channels.html#fig-conv-1x1) shows the cross-correlation computation using the \($1\times 1$\) convolution kernel with 3 input channels and 2 output channels. Note that the inputs and outputs have the same height and width. Each element in the output is derived from a linear combination of elements *at the same position* in the input image. You could think of the \($1\times 1$\) convolutional layer as constituting a fully-connected layer applied at every single pixel location to transform the \($c_i$\) corresponding input values into \($c_o$\) output values. Because this is still a convolutional layer, the **weights are tied across pixel location.** Thus the \($1\times 1$\) convolutional layer requires \($c_o\times c_i$\) weights (plus the bias).

-   equal to 

    ```python
    def corr2d_multi_in_out_1x1(X, K):
        c_i, h, w = X.shape
        c_o = K.shape[0]
        X = X.reshape((c_i, h * w))
        K = K.reshape((c_o, c_i))
        # Matrix multiplication in the fully-connected layer
        Y = torch.matmul(K, X)
        return Y.reshape((c_o, h, w))
    ```

    

-   related: Inception Module

    https://deepai.org/machine-learning-glossary-and-terms/inception-module

    -   Goal: solve the problem of **computational expense, as well as overfitting,** among other issues
    -   The solution, in short, is to **take multiple kernel filter sizes within the CNN**, and **rather than** **stacking them sequentially, ordering them to operate on the same level**. 

-   https://machinelearningmastery.com/introduction-to-1x1-convolutions-to-reduce-the-complexity-of-convolutional-neural-networks/

    >   To address this problem, a 1×1 [convolutional layer](https://machinelearningmastery.com/convolutional-layers-for-deep-learning-neural-networks/) can be used that offers a **channel-wise pooling**, often called **feature map pooling** or a **projection layer**. This simple technique can be used for dimensionality reduction, decreasing the number of feature maps whilst retaining their salient features. It can also be used directly to create a one-to-one projection of the feature maps to pool features across channels or to increase the number of feature maps, such as *after traditional pooling layers*.