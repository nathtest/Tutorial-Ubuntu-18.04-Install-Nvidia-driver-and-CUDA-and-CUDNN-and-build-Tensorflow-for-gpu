# Ubuntu-18.04-Install-Nvidia-driver-and-CUDA-and-CUDNN-and-Tensorflow-gpu-build
Ubuntu 18.04 How to install Nvidia driver + CUDA + CUDNN +  build tensorflow for gpu step by step command line

    1  uname -a
    2  sudo apt-get install openjdk-8-jdk git python-dev python3-dev python-numpy python3-numpy python-six python3-six build-essential python-pip python3-pip python-virtualenv swig python-wheel python3-wheel libcurl3-dev libcupti-dev
    3  sudo add-apt-repository ppa:graphics-drivers/ppa
    4  $ sudo apt update
    5  $ sudo apt-get update
    6  $ sudo apt
    7  $ sudo aptget install
    8  $ sudo apt-get install
    9  $ sudo apt-get install lol
   10  sudo apt install
   11  sudo apt upgrade
   12  lsmod | grep nvidia
   13  $ sudo ubuntu-drivers autoinstall
   14  sudo ubuntu-drivers autoinstall
   15  ubuntu-drivers devices
   16  sudo ubuntu-drivers autoinstall
   17  sudo reboot
   18  sudo apt update-grub
   19  sudo update-gub
   20  sudo update-grub
   21  sudo gedit /etc/default/grub
   22  gcc-6 -v
   23  g++-6
   24  gcc -v
   25  sudo apt-get install gcc-6
   26  sudo apt-get install g++-6
   27  gcc-6
   28  sudo sh cuda_8.0.61_375.26_linux.run --override --silent --toolkit
   29  ls
   30  cd Downloads/
   31  sudo sh cuda_9.0.176_384.81_linux.run --override --silent --toolkit
   32  tar -xzvf cudnn-9.0-linux-x64-v7.1.tgz 
   33  sudo cp cuda/include/cudnn.h /usr/local/cuda/include
   34  sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64
   35  sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn*
   36  ls
   37  gedit ~/.bashrc
   38  sudo ldconfig
   39  echo $CUDA_HOME
   40  source ~/.bashrc
   41  echo $CUDA_HOME
   42  cd  $CUDA_HOME
   43  ls
   44  sudo ldconfig
   45  nvidia-smi
   46  cd /
   47  ls
   48  cd home/
   49  cd nath
   50  echo "deb [arch=amd64] http://storage.googleapis.com/bazel-apt stable jdk1.8" | sudo tee /etc/apt/sources.list.d/bazel.list
   51  curl https://bazel.build/bazel-release.pub.gpg | sudo apt-key add -
   52  sudo apt install curl
   53  curl https://bazel.build/bazel-release.pub.gpg | sudo apt-key add -
   54  sudo apt-get update
   55  sudo apt-get install bazel
   56  sudo apt-get upgrade bazel
   57  cd ~
   58  git clone https://github.com/tensorflow/tensorflow
   59  cd ~/tensorflow
   60  git checkout r1.8
   61  cd ~/tensorflow
   62  ./configure
   63  bazel build --config=opt --config=cuda --incompatible_load_argument_is_label=false //tensorflow/tools/pip_package:build_pip_package
   64  bazel build --config=opt --config=cuda //tensorflow/tools/pip_package:build_pip_package
   65  bazel build --config=opt --config=cuda --action_env="LD_LIBRARY_PATH=${LD_LIBRARY_PATH} //tensorflow/tools/pip_package:build_pip_package
   66  echo $LD_LIBRARY_PATH
   67  bazel build --config=opt --config=cuda --action_env="LD_LIBRARY_PATH=${LD_LIBRARY_PATH}" //tensorflow/tools/pip_package:build_pip_package
   68  sudo echo "/usr/local/cuda/lib64" > /etc/ld.so.conf.d/cuda.conf
   69  bazel build --config=opt --config=cuda --action_env="/usr/local/cuda/lib64" //tensorflow/tools/pip_package:build_pip_package
   70  sudo apt-get update gcc-5
   71  sudo apt-get install gcc-5
   72  sudo apt-get install g++-5
   73  gcc-5
   74  g++-5
   75  ./configure
   76  kill bazel
   77  bazel clean
   78  bazel kill
   79  bazel help
   80  bazel shutdown
   81  ./configure
   82  bazel build --config=opt --config=cuda --action_env="/usr/local/cuda/lib64" //tensorflow/tools/pip_package:build_pip_package
   83  sudo echo "/usr/local/cuda/lib64" > /etc/ld.so.conf.d/cuda.conf
   84  sudo bash -c echo "/usr/local/cuda/lib64" > /etc/ld.so.conf.d/cuda.conf
   85  su
   86  su 
   87  su
   88  sudo bash -c 'echo "/usr/local/cuda/lib64" > /etc/ld.so.conf.d/cuda.conf'
   89  sudo ldconfig
   90  ln -s libcudnn.so.7.* libcudnn.so.7
   91  sudo ln -s libcudnn.so.7.* libcudnn.so.7
   92  sudo ldconfig
   93  cd /usr/local/cuda/lib64
   94  sudo ln -s libcudnn.so.7.* libcudnn.so.7
   95  ln
   96  ln --help
   97  sudo ln -f -s libcudnn.so.7.* libcudnn.so.7
   98  cd /
   99  cd /home/nath/Downloads/
  100  cd ls
  101  cd ..
  102  ls
  103  cd tensorflow/
  104  sudo bash -c 'echo "/usr/local/cuda/lib64" > /etc/ld.so.conf.d/cuda.conf'
  105  bazel build --config=opt --config=cuda --action_env="/usr/local/cuda/lib64" //tensorflow/tools/pip_package:build_pip_package
  106  sudo apt-get install gcc-4
  107  sudo add-apt-repository ppa:ubuntu-toolchain-r/test
  108  sudo apt-get update
  109  sudo apt-get install gcc-4.9
  110  sudo apt-get install gcc-4
  111  apt-get install gcc-4.9
  112  sudo apt-get install gcc-4.9
  113  sudo apt-get update; sudo apt-get install gcc-4.8 g++-4.8
  114  sudo apt-get update; sudo apt-get install gcc-4.9 g++-4.9
  115  sudo apt-get update; sudo apt-get install gcc-4.8 g++-4.8
  116  ./configure
  117  bazel shutdown
  118  python3.6
  119  ./configure
  120  bazel build --config=opt --config=cuda --action_env="/usr/local/cuda/lib64" //tensorflow/tools/pip_package:build_pip_package
  121  ls
  122  bazel-bin/tensorflow/tools/pip_package/build_pip_package tensorflow_pkg
  123  cd tensorflow_pkg/
  124  sudo pip3 install tensorflow-1.8.0-cp36-cp36m-linux_x86_64.whl 
