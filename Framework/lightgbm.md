-   Lightgbm with gpu required recompile 
    -   https://www.thekerneltrip.com/machine-learning/lgbmgpu/

-   official gpu tuning guide
    -   https://lightgbm.readthedocs.io/en/latest/GPU-Performance.html

-   lightgbm **feature importance**

    -   >   **importance_type** (*str**,* *optional* *(**default="split"**)*) – How the importance is calculated. If “split”, result contains numbers of times the feature is used in a model. If “gain”, result contains total gains of splits which use the feature.

    -   https://lightgbm.readthedocs.io/en/latest/pythonapi/lightgbm.Booster.html#lightgbm.Booster.feature_importance