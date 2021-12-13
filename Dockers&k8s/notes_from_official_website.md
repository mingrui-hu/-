#### Docker Desktop

>   Docker Desktop includes the Docker daemon (`dockerd`), the Docker client (`docker`), Docker Compose, Docker Content Trust, Kubernetes, and Credential Helper

#### Dockerfile

>   To build your own image, you create a *Dockerfile* with a simple syntax for defining the steps needed to create the image and run it. 
>
>   Each instruction in a Dockerfile creates a **layer** in the image. 
>
>   When you change the Dockerfile and rebuild the image, only those layers which have changed are rebuilt.

### Containers

>   By default, containers can connect to external networks using the host machine’s network connection.

## Docker Engine

>   ## Installation methods
>
>   You can install Docker Engine in different ways, depending on your needs:
>
>   -   Most users [set up Docker’s repositories](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository) and install from them, for ease of installation and upgrade tasks. This is the recommended approach.
>   -   Some users download the DEB package and [install it manually](https://docs.docker.com/engine/install/ubuntu/#install-from-a-package) and manage upgrades completely manually. This is useful in situations such as installing Docker on air-gapped systems with no access to the internet.
>   -   In testing and development environments, some users choose to use automated [convenience scripts](https://docs.docker.com/engine/install/ubuntu/#install-using-the-convenience-script) to install Docker.
>   -   

## Get started

-   Q: run docker -> train in background?

    -   ```shell
         docker run -d -p 80:80 docker/getting-started
        ```

    -   You’ll notice a few flags being used. Here’s some more info on them:

        -   `-d` - run the container in detached mode (in the background)

-   container image

    >   When running a container, it uses an isolated filesystem. This custom filesystem is provided by a **container image**. Since the image contains the container’s **filesystem**, it must contain everything needed to run an application - all **dependencies, configuration, scripts, binaries**, etc. The image also contains other **configuration** for the container, such as **environment variables, a default command to run, and other metadata**.

    >   If you’re familiar with `chroot`, think of a container as an extended version of `chroot`. The filesystem is simply coming from the image. But, a container adds additional isolation not available when simply using chroot.

-   Q: how to map multiple ports in docker to host machine
    -   i.e. need at least: jupyter port 8000, mlflow port 5000

-   Q: how to launch a terminal in a container

    -   >   You will see **a terminal that is running a shell in the ubuntu container**. Run the following command to see the content of the `/data.txt` file. Close this terminal afterwards again.