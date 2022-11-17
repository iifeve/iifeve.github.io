---
title: 给ubuntu装ros
tags: TeXt
article_header:
  type: cover
  image:
    src: https://i0.wp.com/varhowto.com/wp-content/uploads/2020/05/How-to-Install-ROS-Noetic-on-Ubuntu-20.04.png?w=1199&ssl=1
---

# ros 版本选择

|Ubuntu|ROS1|
|--|--|
|14.04 LTS|indigo lgloo|
|16.04 LTS|Kinetic Kame|
|18.04 LTS|Melodic Morenia|
|20.04 LTS|Noetic Ninjemys(Recommended)|

Noetic Ninjemys 是ROS1的最后一个版本，以后的ROS都是ROS2了。

也就是说官方的ROS1已经不支持Ubuntu22.04了。

于是选择了**Noetic**

# ROS安装过程

1. ### 配置系统软件源
   
   `用来免翻墙的，略`
2. ### 添加ROS源、密钥

```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```

```
sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
```

3. ### 安装ROS

  确保索引是最新的：

```
sudo apt update
```

  使用aptitude进行安装，因为这个语句可以解决一些依赖问题：安装aptitude`sudo apt-get install aptitude`

```
sudo aptitude install ros-noetic-desktop-full
```

给出提示：

```
The following packages have unmet dependencies:
……………………
The following actions will resolve these dependencies:

      Keep the following packages at their current version:   
```

这个提示是在说，有一些包没有依赖，以下方法可以解决

但是有一个坑的地方，**默认解决方法是不再安装**，所以**通过q指令放弃当前建议**，直到以下建议

```
Accept this solution? [Y/n/q/?] n
The following actions will resolve these dependencies:

     Keep the following packages at their current version:       
1)     libcurl4-gnutls-dev [Not Installed]                       

     Downgrade the following packages:                           
2)     libgphoto2-6 [2.5.25-0ubuntu0.1 (now) -> 2.5.24-1 (focal)]

```

接受后即可安装

4. ### 设置环境变量
   
   以下是永久性的设置环境变量：
   ```
   echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
   source ~/.bashrc
   ```
5. 
   
     ### 初始化ROSdep
   
   命令：
   ```
   sudo rosdep init
   ```
   
    报错`sudo: rosdep: command not found`

 解决：

```
sudo apt install python3-rosdep2
报错：
 ERROR: default sources list file already exists:
      /etc/ros/rosdep/sources.list.d/20-default.list
       Please delete if you wish to re-initialize
       解决：`sudo rm /etc/ros/rosdep/sources.list.d/20-default.list`就是给删了
```

 完成初始化后提示需要`update`

```
rosdep update
```

```
此处需要翻墙
```

6. 

```
 ### 安装ROSinstall

 原本是
```

```
sudo apt-get install python-rosinstall python-rosinstall-generator python-wstool build-essential
```

```
 修改为
```

```
sudo apt-get install python3-rosinstall python3-rosinstall-generator python3-wstool build-essential
```

```
 也就是要使用python3而不是python
```

7. 

  ### 加载环境配置并测试

```
echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

测试：初始化一个工作区

```
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/src
catkin_init_workspace
cd ~/catkin_ws/
catkin_make
```

报错：`Unable to find either executable 'empy' or Python module 'em'...  try`

原因：这是因为catkin找的python版本为anaconda下面的版本，所以需要改为指定采用下面的命令

解决： `catkin_make -DPYTHON_EXECUTABLE=/usr/bin/python3`

再次报错：`bash: /opt/ros/noetic/bin/catkin_make: No such file or directory`

```
source ~/catkin_ws/devel/setup.bash
```

8. 

   ### 测试结果

1. 在任意终端启动core
   ```
   roscore
   ```
2. 在新终端运行示例
   ```
   sudo apt install ros-noetic-turtlesim
   rosrun turtlesim turtlesim_node
   ```
3. 键盘控制
   ```
   rosrun turtlesim turtle_teleop_key
   ```
   
   <br/>
   
   
