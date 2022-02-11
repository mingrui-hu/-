### XAI for CNN

-   all methods mentioned can detect sub-sequences

#### Backpropogation-based

-   CAM: class activation mapping
    -   require global pooling layer
-   "Gradient*Input"
    -   for both classification & regression

#### Purtabation-based

-   ConvTimeNet: **occlusion sensitivity** methods -> occludes parts of the time series and compute the difference in y
-   **Counterfactual** methods
    -   Define the importance of each observation as the change in y caused by replacing the observation with a **generated** one

### XAI for RNN

-   Attn on CNN/LSTM
    -   temporal attention
    -   variable attention
    -   ==Did not mention about detecting subsequences==

-   Attn in transformer
    -   claims to be able to detect **globally important variable**s,  **persistent temporal pattern**s, **significant event**s
-   SHAP for RNN

### Data-mining based

-   Fuzzy logic & Symbolic Aggregate Approximation(SAX)

### Representative Examples

-   Shapelet-based 

## Evalution methods

