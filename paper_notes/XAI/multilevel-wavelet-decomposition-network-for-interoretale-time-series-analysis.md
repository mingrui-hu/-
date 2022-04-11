#### 1. learnable multi-level wavelet decompostions

#### 2. use the frequency series as inputs to stacked classifiers/regressors

#### model architecture

-   stacked Residual Classifier Flow

-   stacked multi-frequent LSTM (+DNN for concatenation & prediction)

### 3. interpretation

-   evaluate the frequencies captured by each layers's convolution kernel

-   define input/middle layer importance score : saliency methods in  frequency domain
    -   importance spectra
    -   ==evaluates importance patterns of T-wave on ECG & trends on CellPhone==