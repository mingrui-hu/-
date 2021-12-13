https://www.chrisatmachine.com/Jupyter/01-jupyter-remote/



1.   config password instead of tokens

     ```
     jupyter notebook --generate-config
     jupyter notebook password
     ```

     

2.   start on remote

```shell
jupyter lab --no-browser --ip=0.0.0.0
```





### related

1.   jupyter lab kernel中并未显示conda environments

     -   https://stackoverflow.com/questions/39604271/conda-environments-not-showing-up-in-jupyter-notebook

     -   ```shell
         conda install jupyter
         conda install nb_conda
         conda install ipykernel
         
         # redundant, jupyter can find the kernel after installing the above 3 packages
         python -m ipykernel install --user --name mykernel
         ```

     -   