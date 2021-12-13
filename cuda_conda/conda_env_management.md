-   https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html

### yml

```shell
conda env export > environments.yml
conda env export --from-history > environments.yml
conda env export --no-builds > environments.yml
```

```shell
conda env create -f environments.yml
conda env update --file environments.yml [--prune]
```

ref: https://stackoverflow.com/questions/42352841/how-to-update-an-existing-conda-environment-with-a-yml-file



### requirements.txt 

-   conda & pip3

https://stackoverflow.com/questions/50777849/from-conda-create-requirements-txt-for-pip3

### conda-pack

https://conda.github.io/conda-pack/

https://github.com/conda/conda-pack/issues/98

-   source machine

```shell
# Pack environment my_env into my_env.tar.gz
$ conda pack -n my_env [--ignore-missing-files]

# Pack environment my_env into out_name.tar.gz
$ conda pack -n my_env -o out_name.tar.gz

# Pack environment located at an explicit path into my_env.tar.gz
$ conda pack -p /explicit/path/to/my_env
```

-   target machine

```shell
 # Unpack environment into directory `my_env`
$ mkdir -p my_env
$ tar -xzf my_env.tar.gz -C my_env

# Use python without activating or fixing the prefixes. Most python
# libraries will work fine, but things that require prefix cleanups
# will fail.
$ ./my_env/bin/python

# Activate the environment. This adds `my_env/bin` to your path
$ source my_env/bin/activate

# Run python from in the environment
(my_env) $ python

# Cleanup prefixes from in the active environment.
# Note that this command can also be run without activating the environment
# as long as some version of python is already installed on the machine.
(my_env) $ conda-unpack

# At this point the environment is exactly as if you installed it here
# using conda directly. All scripts should work fine.
(my_env) $ ipython --version

# Deactivate the environment to remove it from your path
(my_env) $ source my_env/bin/deactivate
```

-   pip 临时换源

```shell
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple xxxxxx
```

-   永久配置pip源

-   ```shell
    pip install pip -U
    pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
    ```

    

