-   https://aws.amazon.com/blogs/opensource/why-use-docker-containers-for-machine-learning-development/

-   >   ## What you should and shouldn’t include in your machine learning development container
    >
    >   There isn’t a right answer and how your team operates is up to you, but there are a couple of options for what to include:
    >
    >   1.  **Only the machine learning frameworks and dependencies:** This is the cleanest approach. Every collaborator gets the same copy of the same execution environment. They can clone their training scripts into the container at runtime or mount a volume that contains the training code.
    >   2.  **Machine learning frameworks, dependencies, and training code:** This approach is preferred when scaling workloads on a cluster. You get a single executable unit of machine learning software that can be scaled on a cluster. Depending on how you structure your training code, you could allow your scripts to execute variations of training to run hyperparameter search experiments.

-   >   sharing your development container is also easy. You can share it as a:
    >
    >   1.  **Container image:** This is the easiest option. This allows every collaborator or a cluster management service, such as Kubernetes, to pull a container image, instantiate it, and execute training immediately.
    >   2.  **Dockerfile:** This is a lightweight option. [Dockerfiles](https://docs.docker.com/engine/reference/builder/) contain instructions on what dependencies to download, build, and compile to create a container image. Dockerfiles can be versioned along with your training code. You can automate the process of creating container images from Dockerfiles by using continuous integration services, such as [AWS CodeBuild](https://aws.amazon.com/codebuild/).

-   >   Most upstream repositories build their containers to work everywhere, which means they have to be **compatible with most CPU and GPU architectures**. If you exactly know what system you’ll be running your container on, you’re better off selecting container images that’ve been optimized and qualified for your system configuration.

