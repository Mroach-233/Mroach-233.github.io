---
layout: post
title: "Unity构建apk"
date:   2023-09-01
tags: [Unity]
comments: true
author: Mroach-233
---

之前Android Studio装好了，接下来就是在Unity构建apk，构建的过程可谓一波三折，走了不少弯路，这里都记录一下。

<!-- more -->

## 一、配置SDK、JDK、NDK

1. 构建apk需要事先配置SDK、JDK和NDK路径，依次打开【**Edit**】-【**Preferences**】-【**External Tools**】；

   ![image-20230830112743341](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230830112743341.png)

2. 如果没有上图Android相关的配置，则需要打开【**File**】-【**Build Settings**】，检查Android平台的模块有没有加载，没有的话需要找到**Open Download Page**（或者**Install with Unity Hub**），点击之后跳转到网页（或者Unity hub）下载，下载完成先关闭Unity再安装，安装完成后重启Unity，再打开**Preferences**就能发现Android相关配置的选项；

   ![image-20230830112925548](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230830112925548.png)

4. 打开**Android Studio**，【**File**】-【**Settings**】-【**Languages & Frameworkd**】-【**Android SDK**】，找到SDK路径；

   <img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230830120107368.png" alt="image-20230830120107368" style="zoom:80%;" />

5. JDK路径则在【**File**】-【**Settings**】-【**Build, Execution, Deployment**】-【**Build Tools**】-【**Gradle**】中找到；

   <img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230830142744465.png" alt="image-20230830142744465" style="zoom:80%;" />

6. JDK路径则可以在【**Editor**】-【**Project Structure**】-【**SDK Location**】-【**Android NDK location**】中找到，如果没有安装的话可以点击下面的**Download**下载安装；

   <img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230831174443799.png" alt="image-20230831174443799" style="zoom:80%;" />

6. 然后回到Unity配置相关路径，在配置JDK的时候会出现以下警告，是因为JDK版本太高，需要使用Unity指定的版本才行；

   ![image-20230830150119530](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230830150119530.png)


## 二、重新下载指定版本的JDK、SDK、NDK文件

1. 现在需要下载Unity指定版本的配置文件，可以[官方文档](https://docs.unity3d.com/Manual/android-sdksetup.html)查询到不同版本Unity所支持的文件版本号，打开之后在左上角的版本中选择对应的Unity版本，例如我的是2021.3，就能查询到所支持的文件版本；

   <img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230831195456870.png" alt="image-20230831195456870" style="zoom:80%;" />

2. JDK和SDK的安装参考上一篇安装Android Studio的文章，NDK的下载最好跟Unity列的版本完全一致，指大小版本号都得一致，不然在Unity里配也会报弹窗，各个版本都可以在这个[网站](https://androidsdkoffline.blogspot.com/p/android-ndk-side-by-side-direct-download.html)里下载。下载完后NDK的安装也是无脑下一步；

3. 然后回到Unity重新配置JDK、SDK、NDK，报黄色的警告是说没有从Unity官方下载，如果我们下载的版本是正确的则可以无视警告；

   <img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230831202806248.png" alt="image-20230831202806248" style="zoom:80%;" />


## 三、官方下载

1. 除了手动下载JDK、SDK、NDK进行配置之外，还可以通过Unity hub下载。在Unity hub安装一栏，找到对应的Unity版本，点击右边的按钮，选择添加模块；

   <img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230901105752482.png" alt="image-20230901105752482" style="zoom:80%;" />

2. 可能有的版本没有这个**添加模块**的按钮，原因是这个版本不是从Unity hub下载的，而是从外部导入的。可以找到一个有添加模块选项的版本，然后打开该版本目录，找到**modules.json**这个文件（以2018版本举例）；

   ![image-20230830171117842](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230830171117842.png)

3. 复制**modules.json**，移动到外部导入的版本路径下，然后重命名，用记事本或者其他软件打开；

   3.1 全局搜索**selected**，把**true**通通改成**false**；

   3.2 全局搜索**modules.json**源编辑器版本的前6位（2018.2.3），并按照对应的格式改成外部导入的版本（2021.3.8）；

   3.3 去[Unity官网](https://unity.cn/releases)找到对应2021.3.8的版本，点击**Release notes**；

   <img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230901112006722.png" alt="image-20230901112006722" style="zoom:67%;" />

   3.4 然后找到**Android Target Support**，鼠标右键复制链接，同理如果想要添加其他模块也是一样的操作；

   <img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230830172649082.png" alt="image-20230830172649082" style="zoom:67%;" />

   3.5 接着在**modules.json**里搜索**Android Build Support**，并将**downloadUrl**后面一大串换成刚才复制的链接；

   3.6 重启Unity hub，然后发现有添加模块的选项了；

   3.7 接着选择下载安装**Android Build Support**平台的内容，下载完成后去到配置页面，发现依旧没有下载到JDK、SDK，NDK，白忙活一场，可能是因为需要使用版本一致的**modules.json**文件；

   <img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230901113719077.png" alt="image-20230901113719077" style="zoom:80%;" />

4. 其实还有一种方法，就是先卸载从外部导入的Unity版本，然后重新在Unity hub中下载，也是从[Unity官网](https://unity.cn/releases)下载对应版本，选择**从Hub下载**，然后就会自动打开Unity hub，下载的时候就可以选择所需的平台下载了，完事之后打开配置页面，就会发现已经自动配置好了JDK、SDK、NDK的路径；

   ![image-20230901115616720](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230901115616720.png)

## 四、构建apk

1. 完成JDK、SDK、NDK的配置之后，就能开始着手构建apk了，点击【**File**】-【**Build Settings**】，选择**Android**平台，然后点击**Switch Platform**切换至Android平台；

   <img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230901152044989.png" alt="image-20230901152044989" style="zoom:80%;" />

2. 然后点击**Player Settings**，然后修改**Company Name**和**Product Name**

   <img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230901152620216.png" alt="image-20230901152620216" style="zoom:67%;" />

3. 打开**Resolution and Presentation**，在**Orientation**选项卡里找到**Default Orientation**，这是设置屏幕旋转方向的，从上至下分别代表：竖屏，竖屏（手机倒过来），横屏（摄像头在右手边），横屏（摄像头在左手边），自动旋转；

   ![image-20230901152940061](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230901152940061.png)

4. 然后在**Publishing Settings**里点击**Keystore Manager**；

   <img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230901154803868.png" alt="image-20230901154803868" style="zoom:80%;" />

5. 在弹出的窗口中依次选择【**Keystore...**】-【**Create New**】-【**In Dedicated Location...**】，然后选择保存的位置；

   ![image-20230901160306980](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230901160306980.png)

6. 接着输入密码，需要确保密码一致，**Alias**自己填一个就行，然后就能点击右下角的**Add Key**了。

   <img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230901162823050.png" alt="image-20230901162823050" style="zoom:80%;" />

7. 然后回到之前的界面，填上刚才的信息就行；

   <img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230901163731009.png" alt="image-20230901163731009" style="zoom:80%;" />

8. 然后回到**Build Settings**，点击**Build**就行；

   <img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230901163837457.png" alt="image-20230901163837457" style="zoom:80%;" />

## 参考资料

1. 不同版本的Unity要求的NDK版本和两者对应关系表(Unity NDK Version Match) https://zhuanlan.zhihu.com/p/386471785
2. 官网下载的unity编辑器如何在hub上出现添加模块按钮 https://developer.unity.cn/projects/607f88a4edbc2a1246730b64
3. Unity如何添加模块（SDK,NDK,JDK,设置中文等）https://zhuanlan.zhihu.com/p/371511169
4. unity2019版本的如何打包（或打包时没Build System怎么办） https://blog.csdn.net/qq_57896821/article/details/122065948
