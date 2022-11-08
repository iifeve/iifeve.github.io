---

layout: post
title: 给ubuntu安装cuda

---

环境背景

- 已经安装nvidia的cuda驱动，是系统主动安装的，所以在usr/local/中么有cuda文件夹
- 安装了anaconda，并且用anaconda安装了cudatoolkit，cudnn，但是anaconda安装的这两个不能用来编译cuda算子

流程：

1. 在[官网](https://developer.nvidia.com)找到要安装的版本，一般来说直接搜索CUDA Toolkit + 版本号就是
2. 查找自己电脑的架构，并选择对应的选项下载runfile
   ```
   dpkg --print-architecture
   arch
   file /lib/systemd/systemd
   ```
3. 根据提示安装，结果如下
   ```
   ===========
   = Summary =
   ===========
   
   Driver:   Not Selected
   Toolkit:  Installed in /usr/local/cuda-11.3/
   Samples:  Installed in /home/iifeve/, but missing recommended libraries
   
   Please make sure that
    -   PATH includes /usr/local/cuda-11.3/bin
    -   LD_LIBRARY_PATH includes /usr/local/cuda-11.3/lib64, or, add /usr/local/cuda-11.3/lib64 to /etc/ld.so.conf and run ldconfig as root
   
   To uninstall the CUDA Toolkit, run cuda-uninstaller in /usr/local/cuda-11.3/bin
   ***WARNING: Incomplete installation! This installation did not install the CUDA Driver. A driver of version at least 465.00 is required for CUDA 11.3 functionality to work.
   To install the driver using this installer, run the following command, replacing <CudaInstaller> with the name of this run file:
       sudo <CudaInstaller>.run --silent --driver
   
   Logfile is /var/log/cuda-installer.log
   ```
4. 因为电脑已经安装了515版本的cuda(对应cuda11.7)所以没有安装驱动，根据后续的提示，要设置相应的环境变量
5. 环境变量的设置方式：
   ```
   一次性：
   #export PATH=$PATH:/home/xyz/Tesseract/bintesseract可执行文件目录
   #export LD_LIBRARY_PATH=$LD_LIBRARY_PATH://home/xyz/Tesseract/lib其依赖库lept的路径
   #export TESSDATA_PREFIX=/home/xyz/Tesseract/share其依赖的训练数据文件所在路径
   
   检查：
   #export
   #echo $PATH
   
   永久：
   在~/.bashrc文件中增加一次性的语句
   ```
