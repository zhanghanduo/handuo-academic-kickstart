+++
title = "Install new linux environment"
date = 2018-10-29T14:46:14+08:00
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["Handuo"]

# Tags and categories
# For example, use `tags = []` for no tags, or the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = ["Info"]
categories = []

# Featured image
# Place your image in the `static/img/` folder and reference its filename below, e.g. `image = "example.jpg"`.
# Use `caption` to display an image caption.
#   Markdown linking is allowed, e.g. `caption = "[Image credit](http://example.org)"`.
# Set `preview` to `false` to disable the thumbnail in listings.
[header]
image = ""
caption = ""
preview = false

+++

When you want to install a brand new Ubuntu 16.04 system. You could try to follow this guidance.

1. Open `Software & Updates` and choose the fastest source.

2. Update the system:
```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt-get update
sudo apt-get dist-upgrade
sudo apt-get install build-essential git
```

3. Install Nvidia driver
```
sudo apt-get install nvidia-396 nvidia-settings
```
Under cases you have Intel GPU also, please type:
```
sudo prime-select nvidia
```

4. Clone the dotfile repository:

```
mkdir softwares && cd softwares
https://github.com/zhanghanduo/dotfiles.git
cd dotfiles
```
Then follow the `readme.md` to install necessary packages and change some settings.
Then reboot to make some settings valid.

5. Install CUDA:

Type:

```
sudo chmod a+x cuda_xxx_linux_64.run
sudo ./cuda_xxx_linux_64.run
```

add the following settings to your .zshrc or .bashrc file and **source** it:

```
export PATH=$PATH:/usr/local/cuda/bin
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
export CUDA_HOME=/usr/local/cuda
```

6. Install CUDNN

unzip the CUDNN file:

```
 tar -xzvf cudnn-9.0-linux-x64-v7.tgz
```

Then copy and change permissions:

```
 sudo cp cuda/include/cudnn.h /usr/local/cuda/include
 sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64
 sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn*
```

7. Install ROS Kinetic

```
sudo apt-get install ros-kinetic-desktop-full
sudo rosdep init
rosdep update
sudo apt-get install python-rosinstall python-rosinstall-generator python-wstool
```
add the following settings to your .zshrc file and ** source ** it:
```
source /opt/ros/kinetic/setup.zsh
source ~/.zshrc
```
If you use bash instead of zsh you need to run the following commands to set up your shell:
```
source /opt/ros/kinetic/setup.bash
source ~/.bashrc
```

8. Instal OpenCV 3.x

8.1 Download
OpenCV source codes can be downloaded in [opencv github](https://github.com/opencv/opencv/releases).
OpenCV corresponding contrib can be downloaded in [opencv_contrib github](https://github.com/opencv/opencv_contrib/releases).

8.2 Prerequisites

Before you install OpenCV
```
mkdir release && cd release
sudo apt-get build-dep -y opencv
(Optional) sudo apt-get install python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev
```
8.3 Cmake

For normal configure, just type:
```
cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_TBB=ON -D WITH_V4L=ON -D ENABLE_CXX11=ON -D ENABLE_PRECOMPILED_HEADERS=OFF -D CMAKE_CXX_FLAGS='-std=c++11' ..
```
With contrib, just add: `-D OPENCV_EXTRA_MODULES_PATH=/home/hd/softwares/opencv_contrib-3.4.1/modules`.

With CUDA, just add: `-D WITH_CUDA=ON -D ENABLE_FAST_MATH=1 -D CUDA_FAST_MATH=1 -D WITH_CUBLAS=1 -D CUDA_GENERATION=Auto`.

If you encounter some C++ 11 errors during compiling when you install 3.4 or later, just add: `-D CMAKE_CXX_FLAGS='-std=c++11' -D CUDA_NVCC_FLAGS='-std=c++11 --expt-relaxed-constexpr'` 

8.4 Compiling and installing
```
make -j8
sudo make install
```

8.5 Environment
```
echo '/usr/local/lib' | sudo tee -a /etc/ld.so.conf.d/opencv.conf  
sudo ldconfig  
printf '# OpenCV\nPKG_CONFIG_PATH=$PKG_CONFIG_PATH:/usr/local/lib/pkgconfig\nexport PKG_CONFIG_PATH\n' >> ~/.bashrc  
source ~/.zshrc 
pkg-config --modversion opencv	//check if opencv is installed and its version
```

