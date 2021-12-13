### read csv type mismatch error

-   https://tutorial.dask.org/04_dataframe.html
-   实测 dd.read_csv `error_bad_line=Fasle` + `warning_bad_line=True` 无效， 可能是与上面同样的原因

## categoricals

https://docs.dask.org/en/stable/dataframe-categoricals.html?highlight=dtype#categoricals

-   intro blog

    https://www.datarevenue.com/en-blog/a-short-introduction-to-dask-for-pandas-developers

## config scheduler

https://docs.dask.org/en/latest/scheduler-overview.html#configuring-the-schedulers

```python
dd.compute(num_workers=8)
```

```shell
# or 
from concurrent.futures import ThreadPoolExecutor
with dask.config.set(pool=ThreadPoolExecutor(4)):
    x.compute()
```

### convert pandas df to dask df

https://stackoverflow.com/questions/39721800/convert-pandas-dataframe-to-dask-dataframe

