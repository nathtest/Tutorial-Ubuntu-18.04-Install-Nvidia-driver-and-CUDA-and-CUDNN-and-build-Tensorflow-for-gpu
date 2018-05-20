# Ubuntu-18.04 Install Nvidia driver and CUDA and CUDNN and build Tensorflow for gpu
Ubuntu 18.04 Tutorial : How to install Nvidia driver + CUDA + CUDNN +  build tensorflow for gpu step by step command line

Install neccesary library :

```
   sudo apt-get install openjdk-8-jdk git python-dev python3-dev python-numpy python3-numpy python-six python3-six build-essential python-pip python3-pip python-virtualenv swig python-wheel python3-wheel libcurl3-dev libcupti-dev
    
    
```
# Install nvidia driver #

Add graphics drivers to your source list :
```
    sudo add-apt-repository ppa:graphics-drivers/ppa
    sudo apt update
    sudo apt upgrade
   
```
 Check what driver will be installed :
```
        ubuntu-drivers devices
   ```
 Auto install latest driver (it will do everything blacklist drivers nouveau , create nvidia daemon  , ect ...) :
   ```
    sudo ubuntu-drivers autoinstall
   ```
   Then reboot your machine :
   ```
    sudo reboot
   ```
   If you boot without any kernel crash you're ok but you can check the correct install of the driver :
   ```
     lsmod | grep nvidia
   
```
  or

```
    nvidia-smi

```
# Install cuda # 

Download cuda_your_cuda_version.run on https://developer.nvidia.com/cuda-toolkit and install it: 

```
     cd Downloads/
     sudo sh cuda_9.0.176_384.81_linux.run --override --silent --toolkit
   
```
If everything is ok you should see a cuda folder in /usr/local/ .

Download linux cudnn_your_version on https://developer.nvidia.com/cudnn and install it:

```
     tar -xzvf cudnn-9.0-linux-x64-v7.1.tgz 
     sudo cp cuda/include/cudnn.h /usr/local/cuda/include
     sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64
     sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn*
   
   
```
Check if you have correctly copied cudnn in /usr/local/cuda/lib64/.

Now you must add some path to your  /.bashrc :

```
     gedit ~/.bashrc
   
 ```
 Add those line at the end of your /.bashrc :
 
  ```
 export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/local/cuda/lib64:/usr/local/cuda/extras/CUPTI/lib64"
 export CUDA_HOME=/usr/local/cuda
  ```
  Now reload your terminal config :
 ```
     sudo ldconfig
  ```
Check if the path are correctly installed :
     
 ```
     echo $CUDA_HOME
 ```
 # Build tensorflow with Bazel #
 
Install bazel :

```
 echo "deb [arch=amd64] http://storage.googleapis.com/bazel-apt stable jdk1.8" | sudo tee /etc/apt/sources.list.d/bazel.list
 curl https://bazel.build/bazel-release.pub.gpg | sudo apt-key add -
 sudo apt install curl
 curl https://bazel.build/bazel-release.pub.gpg | sudo apt-key add -
 sudo apt-get update
 sudo apt-get install bazel
 sudo apt-get upgrade bazel
   
```
Download tensorflow and choose what branch you want :

```
     cd ~
     git clone https://github.com/tensorflow/tensorflow
     cd ~/tensorflow
     git checkout r1.8
     cd ~/tensorflow
  
```

 Create symbolic link for bazel :

```
    sudo bash -c 'echo "/usr/local/cuda/lib64" > /etc/ld.so.conf.d/cuda.conf'
    sudo ldconfig
```
Install gcc 4.8 (only version of gcc that can currently compile tensorflow) :

```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get install gcc-4.8 g++-4.8
  
```
Create configuration file for tensorflow build :

```
    ./configure
  
```
Say no to most query just specify the python version you want , yes to jemalloc and specify correct path to gcc-4.8.

To help you can see my generated config file (.tf_configure.bazelrc ):

```
build --action_env PYTHON_BIN_PATH="/usr/bin/python3"
build --action_env PYTHON_LIB_PATH="/usr/lib/python3/dist-packages"
build --force_python=py3
build --host_force_python=py3
build --python_path="/usr/bin/python3"
build --define with_jemalloc=true
build:gcp --define with_gcp_support=true
build:hdfs --define with_hdfs_support=true
build:s3 --define with_s3_support=true
build:kafka --define with_kafka_support=true
build:xla --define with_xla_support=true
build:gdr --define with_gdr_support=true
build:verbs --define with_verbs_support=true
build --action_env TF_NEED_OPENCL_SYCL="0"
build --action_env TF_NEED_CUDA="1"
build --action_env CUDA_TOOLKIT_PATH="/usr/local/cuda"
build --action_env TF_CUDA_VERSION="9.0"
build --action_env CUDNN_INSTALL_PATH="/usr/local/cuda-9.0"
build --action_env TF_CUDNN_VERSION="7"
build --action_env TF_NCCL_VERSION="1"
build --action_env TF_CUDA_COMPUTE_CAPABILITIES="3.0"
build --action_env LD_LIBRARY_PATH=":/usr/local/cuda/lib64:/usr/local/cuda/extras/CUPTI/lib64"
build --action_env TF_CUDA_CLANG="0"
build --action_env GCC_HOST_COMPILER_PATH="/usr/bin/gcc-4.8"
build --config=cuda
test --config=cuda
build --define grpc_no_ares=true
build:opt --copt=-march=native
build:opt --host_copt=-march=native
build:opt --define with_default_optimizations=true
build --copt=-DGEMMLOWP_ALLOW_SLOW_SCALAR_FALLBACK
build --host_copt=-DGEMMLOWP_ALLOW_SLOW_SCALAR_FALLBACK
```

Build tensorflow with bazel :

```
bazel build --config=opt --config=cuda --action_env="/usr/local/cuda/lib64" //tensorflow/tools/pip_package:build_pip_package
    
```
Create .whl for pip install :

```
    bazel-bin/tensorflow/tools/pip_package/build_pip_package tensorflow_pkg
    cd tensorflow_pkg/
    sudo pip3 install tensorflow-<name_of_generated_file>.whl 
  
```

Thoses steps allowed me to build tensorflow for gpu with a comptute capabilities of 3.0 on a laptop with a GeForce 740m and on ubuntu 18.04.
I hope it can help you as well.
Let me know if you find some quicker way.
