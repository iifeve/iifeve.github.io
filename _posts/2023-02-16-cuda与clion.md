---
title: cuda与clion：正常情况下不会报错但是clion中会报错
tags: cuda;clion
article_header:
  type: cover
  image:
    src: https://cmake.org/wp-content/uploads/2018/11/cmake_logo_slider.png
---

### No CMAKE_CUDA_COMPILER could be found

解决：
在cmake options中写入-DCMAKE_CUDA_COMPILER:PATH=/usr/local/cuda-11.3/bin/nvcc

### 由于cmakecache产生的报错

- 特征：花里胡哨，一般都是在clion的cmake中报错，而在clion外使用编译则不会报错
- 解决方法：Clion - 工具 - 清除cmakecache后重新编译。

### clion无法链接到第三方库
首先确定compile那里有没有设定debug或者release，若设定好的，那么Clion - 工具 - 清除cmakecache后重新编译。
