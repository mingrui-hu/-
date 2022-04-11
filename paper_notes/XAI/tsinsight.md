-   Summary

    -   1.   Goal: substract sparse features guided by the trained classifier
        2.   basically similar to lime in that:
             -   RidgeRegression -> AutoEncoder + contraction norm(?) + sparsity norm
             -   Soft label from the classifier -> directly finetune with the classifier
        3.   claim to be 
             -   global intepretation in that the AE can trained for the whole time-series datasets
             -   local inerpretation in that the AE can be fintuned for the single sample(doubt: overfitting? no sampling of neighborhood samples required? as in lime & shap?)
        4.   feature importance measure: directly use the **output value** of the decoder 

    -   Problems:

        -   1.   autoencoder treat each time step as i.i.d., hence intrinsiclly not suitable for time series,

                 and the results shown in the paper are mostly from the synthetic anomaly datasets, which only contains point anomaly, hence this method will work( in this sense, any ordinary feature attribution method might work). Doubt if it will work on classification heavily relies on the history(trends, seasonal, etc.)

        -   2.   feature attribution: directly used the **output value** of the decoder -> no theory backup,

                 cannot compare btw two models, ==cannot compare btw features(? since the magnitude relies on the input scale?)==, 