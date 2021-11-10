- view tracking ui:
  - `mlflow ui`
  - if needs to **view from other machines**, run `mlflow ui --host 0.0.0.0`
- One Experiment, 2 run
  - running the same script twice with output file of identical name, can also be recorded.  

![image-20210909144912262](D:\笔记\mlflow\tracking-ui.assets\image-20210909144912262-16311701545871.png)

- run MLflow projects

  - MLFlow Projects: code + dependencies -> a package = code + 1 `MLproject` file

  - MLproject =  (dependencies (e.g. python environment)) + (cmds that can be run into the project and arguments they take)

  - ```shell
    mlflow run sklearn_elasticnet_wine -P alpha=0.5
    # run from a GitHub URI
    mlflow run https://github.com/*****.git -P alpha=5.0
    ```

  - if not `tracking server` configured -> projects' Tracking API data in the local `mlrun` directory

 

- Saving & Serving Models

  output: `MLmodel` file -> model description

  ![image-20210909155704771](D:\笔记\mlflow\tracking-ui.assets\image-20210909155704771-16311742262062.png)