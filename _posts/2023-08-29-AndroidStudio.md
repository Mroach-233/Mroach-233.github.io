---
layout: post
title: "Android Studio"
date:   2023-08-29
tags: [Android Studio]
comments: true
author: Mroach-233
---

因为Unity项目需要导出apk，所以需要安装Android Studio，这边稍微记录下安装过程；

<!-- more -->

## 一、JDK

1. 去[官网](https://www.oracle.com/java/technologies/downloads/)下载JDK，我这下的是JKD 17；

   <img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230829161236408.png" alt="image-20230829161236408" style="zoom: 80%;" />

2. 下载完成后双击安装，我这边安装路径选择默认，只不过换成了D盘。因为下载的是exe文件，安装过程会自动配置环境，后续就不用手动配了；

   <img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230829161732136.png" alt="image-20230829161732136" style="zoom: 80%;" />

3. 打开cmd命令行，输入**javac -version**，打印出版本号就证明JDK已经安装成功，并且环境配置也是好的；

   ![image-20230829162214364](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230829162214364.png)

## 二、安装Android Studio

1. 去[官网](https://developer.android.google.cn/studio)下载Android Studio，往下滑就能各平台的下载文件；

   <img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230829164258983.png" alt="image-20230829164258983" style="zoom: 67%;" />

2. 双击安装，也是默认路径，不过是换成D盘；

   <img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230829172100752.png" alt="image-20230829172100752" style="zoom:80%;" />

3. 安装完之后，直接运行启动，在这个页面选择**Custom**，不然后续的SDK会下到C盘里；

   <img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230829200623870.png" alt="image-20230829200623870" style="zoom:80%;" />

4. 接下来就是自定义SDK路径；

   <img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230829201006693.png" alt="image-20230829201006693" style="zoom:80%;" />

5. 到了这步，需要点击右边的列表，然后点击**Accept**，这时候带红色的星号消失，接受完全部之后就能点击**Finish**了；

   <img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230829201228166.png" alt="image-20230829201228166" style="zoom:80%;" />

6. 然后等待下载安装相关的组件，出现这个页面点击**Finish**就可以了;

   <img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230829201529585.png" alt="image-20230829201529585" style="zoom:80%;" />

7. 之后会启动Android Studio，由于是第一次使用，这里选择**New Project**；

   <img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230829201926915.png" alt="image-20230829201926915" style="zoom:80%;" />

8. 这里使用默认的**Empty Activity**，然后点击**Next**;

   <img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230829202107349.png" alt="image-20230829202107349" style="zoom:80%;" />

9. 接着改下项目名字跟项目路径，然后点击**Finish**；

   <img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230829202245322.png" alt="image-20230829202245322" style="zoom:80%;" />

10. 进到项目页面之后，又是漫长的下载和等待，这里是下载gradle，什么时候完成取决于网络环境；

    <img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230829202613624.png" alt="image-20230829202613624" style="zoom: 80%;" />

11. 编译完成，点击运行；

    ![image-20230830092938458](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230830092938458.png)

12. 第一次启动虚拟机花费的时间比较长，启动完成之后会自动运行项目，当看到虚拟机出现”Hello Android“就表示成功了；

    <img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230830094817573.png" alt="image-20230830094817573"  />

## 参考资料

1. Android Studio 安装配置教程 - Windows(详细版) https://blog.csdn.net/qq_38436214/article/details/105073213