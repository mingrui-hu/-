

-   Software - captum
-   Problem Defination:
    -   not a seq-to-seq problem: seq -> single-value-output prediction
-   Compare saliency-based methods: 
    -   pertubation-based: 
        -   Feature Occlusion(adjusted for time series)
        -   Feature Ablation(FA)
        -   Feature Pertubation
    -   gradient-based
        -   GRAD, Integrated Gradients, SmoothGrad, DeepLIFT, ==GradientSHAP==, **==DeepSHAP==**(DeepLift + Shap)
    -   Shapley Values:
        -   Shapley value Sampling
-   Goal: 
    -   ==Feature Importance== at ==a== given time
    -   changes of feature importance over time
-   Considered Network:
    -    LSTM, LSTM-with-input-attention, TCN, Transformers
-   Propose: Two-Phase temporal rescaling approach 

-   Datasts: Synthetic time series datasets with informative features' positions known in advance
-   Conclustion:
    -   1.   saliency methods **cannot distinguish** feature importance ==at== a given time step
             -   ==comment:== ==features's saliency value are highly correlated at the given time step==
        2.   **model architecture** has significant effect on the quality of saliency maps
             -   ==comment:== not surprised - as saliency maps were designed for convolution 

-   Cons:

    -   still, this paper does not analysis **what kind of time events** can the saliency map methods can capture, only anomaly ones with peaks?

    -   do not make statement about robustness to high-freq noises? peak noises(especially when the expected event signal is also peak -> so that cannot apply a low-freq filter first)?
    -   Discussion/analysis on their dataset features(& their proposed questions to consider))& multivariate properties & comparisons btw results are vague.