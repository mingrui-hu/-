## sklearn feature importance

- gini importance
- https://blog.csdn.net/jin_tmac/article/details/87939742?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task
- https://www.jianshu.com/p/405371569156
- https://scikit-learn.org/stable/auto_examples/ensemble/plot_forest_importances.html

```python
    @property
    def feature_importances_(self):
        """Return the feature importances.

        The importance of a feature is computed as the (normalized) total
        reduction of the criterion brought by that feature.
        It is also known as the Gini importance.

        Warning: impurity-based feature importances can be misleading for
        high cardinality features (many unique values). See
        :func:`sklearn.inspection.permutation_importance` as an alternative.

        Returns
        -------
        feature_importances_ : ndarray of shape (n_features,)
            Normalized total reduction of criteria by feature
            (Gini importance).
        """
        check_is_fitted(self)

        return self.tree_.compute_feature_importances()
```

