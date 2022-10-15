---
layout: post
title: cuda|ninja|pytorch|睡眠不足!
mathjax: true # false (default), true
mathjax_autoNumber: true # false (default), true
---
## 遇到的报错

<br/>

## 一堆报错的时候，该如何检查

报了很多错，且不是自己写的代码出错，在C++中表现是头文件、const等，那么可能是环境没配好。

1. 检查warning，特别是最开始报的warning，看看有没有说版本的问题
2. 检查好warning后，先保存warning内容，去查找版本间对应关系
3. 在确定版本间对应关系的条件下，复制新的虚拟环境进行试验
   - `conda create -n BBB --clone AAA`
   - 注：也可以新建一个环境实验：`conda create -n your_env_name python=x.x`
4. 查找之前warning的具体内容，在查找的时候以刚刚获得的经验为导向，不要看见一个试一个

## 环境配置的逻辑

==在使用conda的情况下，环境可以分为系统环境和虚拟环境，其中系统环境由系统的环境变量决定使用哪一个文件夹==

可以参考[windows下安装多个版本cuda](https://blog.csdn.net/zsc201825/article/details/91149550)以及切换使用

关于cuda：是一个并行计算平台和编程模型，能够使得使用GPU进行通用计算变得简单和优雅。

- CUDA Toolkit：
  - Compiler: CUDA-C和CUDA-C++编译器NVCC位于bin/目录中。它建立在NVVM优化器之上，而NVVM优化器本身构建在LLVM编译器基础结构之上。因此开发人员可以使用nvm/目录下的Compiler SDK来直接针对NVVM进行开发。

  - Tools: 提供一些像profiler,debuggers等工具，这些工具可以从bin/目录中获取

  - Libraries: 下面列出的部分科学库和实用程序库可以在lib/目录中使用(Windows上的DLL位于bin/中)，它们的接口在include/目录中可获取。
  - CUDA Driver: 运行CUDA应用程序需要系统至少有一个具有CUDA功能的GPU和与CUDA工具包兼容的驱动程序。
- nvcc&nvidia-smi
  - nvcc其实就是CUDA的编译器,可以从CUDA Toolkit的/bin目录中获取,类似于gcc就是c语言的编译器。
  - 它是一个基于前面介绍过的NVIDIA Management Library(NVML)构建的命令行实用工具，旨在帮助管理和监控NVIDIA GPU设备。
  - 这两个有时候会显示cuda版本不同，CUDA有两个主要的API：runtime(运行时) API和driver API。这两个API都有对应的CUDA版本（如9.2和10.0等）。
- cudnn：
  - 不需要安装，下载压缩包后解压到cuda安装目录就行，cuda安装时选择精简安装的话，会自动安装到[c盘中](https://)，无论一开始选择的安装包是在哪
  - 其实就是一个专门为深度学习计算设计的软件库，里面提供了很多专门的计算函数，如卷积等。

在配置的时候可以同时安装多个版本，为了应付报错

## 参考

[显卡，显卡驱动,nvcc, cuda driver,cudatoolkit,cudnn到底是什么？](https://zhuanlan.zhihu.com/p/91334380)
