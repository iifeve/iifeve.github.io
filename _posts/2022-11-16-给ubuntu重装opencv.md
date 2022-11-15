---
title: 给ubuntu重装opencv
tags: TeXt
article_header:
  type: cover
  image:
    src: /screenshot.jpg
---

## 报错内容：

```
cv2.error: OpenCV(4.6.0) /io/opencv/modules/highgui/src/window.cpp:1250: error: (-2:Unspecified error) The function is not implemented. Rebuild the library with Windows, GTK+ 2.x or Cocoa support. If you are on Ubuntu or Debian, install libgtk2.0-dev and pkg-config, then re-run cmake or configure script in function 'cvNamedWindow'
```

## 大致的原因：

opencv安装后没有编译，或者编译出错，或者有依赖的包没有安装

### 如何检查：

1. 首先查看自己是如何安装的opencv，以下三个一次递进，如果pip没有而conda有那么说明conda安装的opencv……
   1. 查看是否由pip安装`pip list | grep opencv`
   2. 查看是否由conda安装`conda list | grep opencv`
   3. 查看是否由ubuntu直接安装`dpkg -l | grep opencv`
2. 找到自己安装的opencv的版本：`Found existing installation: opencv-python-headless 4.6.0.66`，这个[是pycharm直接安装的opencv](https://blog.csdn.net/xhltk316/article/details/118692659)
3. 尝试解决：发现问题是安装的服务器版本的`opencv-python-headless 4.6.0.66`，于是使用pip进行卸载，并重新安装`opencv` 和`opencv-contrib` ，[参考](https://blog.csdn.net/t18438605018/article/details/112297603)

### 总结：

1. [pip与conda 安装的不同](https://www.zhihu.com/question/395145313)，[apt-get与编译安装的不同](https://blog.csdn.net/zou_albert/article/details/112600983)：
   
   conda安装到`anaconda3/pkgs`中，pip安装到`anaconda3/envs/current_env/lib/python3.x/site-packages`中，如果是base环境，就会安装到`~/.local/lib/python3.x/site-packages`中
   
   sudo apt，位置上：安装目录由包的维护者确定
   
     系统安装软件一般在`/usr/share`
   
     可执行的文件在`/usr/bin`
   
     配置文件可能安装到了`/etc`下等
   
     文档一般在` /usr/share`；
   
     可执行文件` /usr/bin`；
   
     lib文件 `/usr/lib`。
 其他方面：会自动处理依赖关系
   
   源码编译安装：
   
   首先安装位置需要自己确定，环境变量/以来关系由自己确定
