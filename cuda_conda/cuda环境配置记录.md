



## ubuntu 20.04 + cuda 11.3 + cuDNN 8.2.1 + miniconda

- ubuntu 20.04 

#### REF

- https://cyfeng.science/2020/05/02/ubuntu-install-nvidia-driver-cuda-cudnn-suits/
- https://docs.nvidia.com/cuda/archive/11.3.1/cuda-installation-guide-linux/index.html#advanced-setup
- https://developer.nvidia.com/rdp/cudnn-archive
- [how  to install nvidia drivers on ubuntu 20.04](https://linuxconfig.org/how-to-install-the-nvidia-drivers-on-ubuntu-20-04-focal-fossa-linux)

- https://beyondstateoftheart.medium.com/install-cuda-toolkit-install-nvidia-driver-ubuntu20-04-1634685ed68a
- [Ubuntu 20.04 安装 CUDA Toolkit 的三种方式](https://www.cnblogs.com/klchang/p/14353384.html)

##### miniconda

- https://docs.conda.io/projects/conda/en/latest/user-guide/configuration/admin-multi-user-install.html
- https://stackoverflow.com/questions/27263620/how-to-install-anaconda-python-for-all-users

- https://medium.com/@pjptech/installing-anaconda-for-multiple-users-650b2a6666c6



## STEP1 CUDA Driver

- 简单方式 `sudo ubuntu drivers auto-install`

  - 查看推荐的版本`ubuntu-drivers devices`

  ![image-20211110112804681](D:\笔记\cuda\cuda环境配置记录.assets\image-20211110112804681-16365148862211.png)

  - 这种方式不需要按照nvidia 的 installation guide去手动禁用原生gpu驱动

  - 查看是否已安装

    ```shell
    dpkg -l | grep -i nvidia
    ```

  - 查看gcc版本 9.3.0

    ```shell
    gcc --version
    ```

    ![image-20211110113520847](D:\笔记\cuda\cuda环境配置记录.assets\image-20211110113520847-16365153228282.png)

  - 检查ubuntu版本

    ```shell
    lsb_release -a
    ```

    <img src="D:\笔记\cuda\cuda环境配置记录.assets\image-20211110134446092.png" alt="image-20211110134446092" style="zoom:50%;" />

  - 检查(并安装)kernel headers

    ```shell
    sudo apt-get install linux-headers-$(uname -r)
    ```

    ![image-20211110113653794](D:\笔记\cuda\cuda环境配置记录.assets\image-20211110113653794-16365154148563.png)

  - 注意安装完成后需要reboot生效， 否则还是开源 `nouvoue` drivers

    `lshw`

    ![image-20211110134819180](D:\笔记\cuda\cuda环境配置记录.assets\image-20211110134819180-16365233009615.png)

    会导致

    ![image-20211110135006604](D:\笔记\cuda\cuda环境配置记录.assets\image-20211110135006604.png)

    reboot 后

    ![image-20211110135134931](D:\笔记\cuda\cuda环境配置记录.assets\image-20211110135134931.png)

  - 确认驱动安装完成

    `nvidia-smi`

    ![image-20211110135153970](D:\笔记\cuda\cuda环境配置记录.assets\image-20211110135153970-16365235153588.png)

## STEP2 安装cuda toolkit

- 方式一： 直接ubuntu源安装 -- 不考虑 -- 只有10.1 

  ```shell
  sudo apt search nvidia-cuda-toolkit
  ```

  <img src="D:\笔记\cuda\cuda环境配置记录.assets\image-20211110135320777.png" alt="image-20211110135320777" style="zoom:50%;" />

- 方式二： 将nvidia cuda添加至sudo apt 源，下载 -- **失败**， developer.nvidia.com 速度只有kb

  步骤如下：

  1. debian installer 

     ! to decide <distro>-<version>-<architecture>: https://developer.download.nvidia.cn/compute/cuda/repos/ubuntu2004/x86_64/

     ```shell
     # sudo dpkg --install cuda-repo-<distro>-<version>.<architecture>.deb
     sudo dpkg --install cuda-repo-ubuntu2004-11-3-11.3.1-1.amd64.deb
     ```

  2. 公钥

     ```shell
     sudo apt-key adv --fetch-keys
     ```

     ![image-20211110140339751](D:\笔记\cuda\cuda环境配置记录.assets\image-20211110140339751-163652422159610.png)

  3. 下载cuda

     ```shell
     sudo apt-get update
     sudo apt-get install cuda
     ```

     ![image-20211110140440972](D:\笔记\cuda\cuda环境配置记录.assets\image-20211110140440972-163652428267111.png)

     ![image-20211110140504546](D:\笔记\cuda\cuda环境配置记录.assets\image-20211110140504546-163652430596512.png)

     其中，查看现有cuda版本：

     ```shell
     sudo apt list -a cuda
     ```

     <img src="D:\笔记\cuda\cuda环境配置记录.assets\image-20211110140219828.png" alt="image-20211110140219828" style="zoom:50%;" />

  - **结果： 下载失败**

    ![image-20211110140928553](D:\笔记\cuda\cuda环境配置记录.assets\image-20211110140928553.png)

- 方式三： Runfile 安装

  - 

    1. 下载runfile

       从https://developer.nvidia.com/cuda-11-3-1-download-archive找到runfile

       ```shell
       wget https://developer.download.nvidia.com/compute/cuda/11.3.1/local_installers/cuda_11.3.1_465.19.01_linux.run
       ```

    2.  ```shell
        sudo sh cuda_11.3.1_465.19.01_linux.run
        ```

       因为已经安装drivers， 此处跳过drivers安装

       ![image-20211110141301927](D:\笔记\cuda\cuda环境配置记录.assets\image-20211110141301927-163652478372013.png)

    			3. 配置

          ```shell
          export PATH=/usr/local/cuda-11.3/bin${PATH:+:${PATH}}
          export LD_LIBRARY_PATH=/usr/local/cuda-11.3/lib64{LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}
          ```

    			4. 确认安装完成

          ```shell
          nvcc --version
          ```

    			5. 按照installation guide 跑demo

          - 注意因为前面安装时并没有配置V100 for display(见installation guide)， 所以会有三方库欠缺或者报错

          ```shell
          cd ~/NVIDIA_CUDA-11.3_Samples/5_Simulations/nbody
          make
          ./nobody
          ```

          ![计算机生成了可选文字: mingrui@fintechkg01:N/NVIDIACUDA-11.3Samples/5Simulations/nbody$make >>>WARNING-IIbGL.sonotfound，refertoCUDAGettingStartedGuIdefor howtofundandInstallthem.<<< >>>WARNING-IIbGLU.sonotfound，refertoCUDAGettingStartedGuIdefo rhowtofundandInstallthem.<<< >>>WARNING-gl．hnotfound，refertoCUDAGettingStartedGuIdeforhow tofundandInstallthem.<<< >>>WARNING-glu.hnotfound，refertoCUDAGettingStartedGuIdeforho WtofundandInstallthem.<<< [@]/usr/local/cuda/bin/nvcc-cc-bin g++．I．．/．./common/tnc ．m64-ftz=true -threads0-gencodearch—compute35，code=sm35 -gencodearch—compute37](D:\笔记\cuda\cuda环境配置记录.assets\clip_image001-163652500574514.png)

          ```shell
          sudo  apt-get install libglu-mesa libglu
          
          # Get start guide 9.3 Optionals
          sudo apt-get install g++ freeglut3-dev build-essential libx11-dev \
              libxmu-dev libxi-dev libglu1-mesa libglu1-mesa-dev 1-mesa-dev
          ```

          run with -benchmark （否则报错因为没有display）

          ![image-20211110142005631](D:\笔记\cuda\cuda环境配置记录.assets\image-20211110142005631-163652520715717.png)

- 最后， 检查软链(我们只有一个版本，不需要修改)

  ![image-20211110142056400](D:\笔记\cuda\cuda环境配置记录.assets\image-20211110142056400.png)

## STEP3 安装cuDNN

- 找到合适版本

  https://developer.nvidia.com/rdp/cudnn-archive

  https://developer.nvidia.com/compute/machine-learning/cudnn/secure/8.2.1.32/11.3_06072021/cudnn-11.3-linux-x64-v8.2.1.32.tgz

  注意，这个需要注册账号下载，不能直接wget

- ```shell
  sudo cp cuda/include/cudnn.h /usr/local/cuda-11.3/include
  
  sudo cp cuda/lib64/libcudnn* /usr/local/cuda-11.3/lib64
  
  sudo chmod a+r /usr/local/cuda-11.3/include/cudnn.h /usr/local/cuda-11.3/lib64/libcudnn*
  ```

## STEP4 配置多用户miniconda

1. 下载 https://repo.anaconda.com/miniconda/Miniconda3-py39_4.10.3-Linux-x86_64.sh

2. ```shell
   adduser miniconda
   ```

2. ```shell
   sudo mkdir /opt/anaconda && sudo chmod ugo+w /opt/anaconda
   ```

3. 安装

   ![image-20211110142614343](D:\笔记\cuda\cuda环境配置记录.assets\image-20211110142614343-163652557588218.png)

   ![image-20211110143214701](D:\笔记\cuda\cuda环境配置记录.assets\image-20211110143214701.png)

   ![image-20211110143319259](D:\笔记\cuda\cuda环境配置记录.assets\image-20211110143319259-163652600077519.png)

4. 修改/etc/profile -> 所有iteractive login用户可以使用

   ```
   # >>> conda initialize >>>
   # !! Contents within this block are managed by 'conda init' !!
   __conda_setup="$('/opt/YOUR_CONDA_DISTRIB_NAME/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
   if [ $? -eq 0 ]; then
       eval "$__conda_setup"
   else
       if [ -f "/opt/YOUR_CONDA_DISTRIB_NAME/etc/profile.d/conda.sh" ]; then
           . "/opt/YOUR_CONDA_DISTRIB_NAME/etc/profile.d/conda.sh"
       else
           export PATH="/opt/YOUR_CONDA_DISTRIB_NAME/bin:$PATH"
       fi
   fi
   unset __conda_setup
   # <<< conda initialize <<<
   
   ```

   

5. 关掉conda 自动激活base - 注意这个是在root账号下完成

   ```shell
   conda config --set auto_activate_base false
   ```

   

## STEP5 安装cuda -- 使用miniconda账号配置

```shell
conda install pytorch torchvision torchaudio cudatoolkit=11.3 -c pytorch
```

