---
title: ubuntu安装cudnn
tags: cuda
article_header:
  type: cover
  image:
    src: https://i0.wp.com/kumarvinay.com/wp-content/uploads/2020/05/Screenshot-2020-05-01-at-9.55.57-PM.png?w=957&ssl=1
---

### 坑
不可以下载官网的安装版(deb)，[详细过程](https://blog.csdn.net/Lucifer_zzq/article/details/76675239)

### 安装过程
要下载压缩包，内容为头文件和动态库，复制到cuda后，直接在环境中链接就行。==为了防止cuda 出问题，把cuda-11.3拷贝到了Env中==
把cudnn中的头文件复制到cuda的头文件下
把cudnn中的库文件复制到cuda下的lib64下
```
export LD_LIBRARY_PATH=/usr/local/cuda-11.3/lib64:$LD_LIBRARY_PATH
```

### 最终结果
下载了 Local Installer for Linux x86_64 (Tar)

链接到了/home/iifeve/Env/cudnn/lib，修改环境变为左边
