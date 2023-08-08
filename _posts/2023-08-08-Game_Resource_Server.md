---
layout: post
title: "游戏资源服务器下载"
date:   2023-08-08
tags: [资源下载]
comments: true
author: Mroach-233
---

先前用云服务器做内网穿透远程连接了家里的电脑，恰好之前到了打Bundle跟解Bundle的环节，以前是用**NetBox2**在本地架设了一个服务器，现在可以试试把Bundle放到云服务器上访问下载了。

<!-- more -->

## 一、下载Apache

Apache的[下载地址](https://httpd.apache.org/)，因为服务器装的是**Windows系统**，所以选择Windows的版本进行安装；

![image-20230808233650028](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230808233650028.png)

![image-20230808142718414](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230808142718414.png)

![image-20230808142735069](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230808142735069.png)

![image-20230808142803293](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230808142803293.png)

## 二、配置文件

1. 解压到任意文件夹，根目录大致如下；

   ![image-20230808143206372](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230808143206372.png)

2. 修改**Apache24\conf**路径下的**httpd.conf**文件，搜索**Define SRVROOT**，把原先根目录的相对路径替换成绝对路径，顺带一提，路径的斜杠最好跟配置文件的一致，使用 ‘**/**’；

   ![image-20230808233826773](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230808233826773.png)

   

3. **httpd.conf**文件里搜索**80**，换成一个别的没被占用的端口，例如**81**；

   ![image-20230808144305904](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230808144305904.png)

4. 继续在**httpd.conf**文件里搜索**DocumentRoot**，这个目录是网站的文件目录，默认是放在**htdocs**文件夹内，也可以自定义修改，这里选择了自定义；

   ![image-20230808230012962](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230808230012962.png)

   

## 三、安装Apache

1. 在命令行（**管理员权限**）中打开到**bin**目录，例如

   ```shell
   cd D:\Users\Mroach\Desktop\httpd-2.4.55-o111s-x64-vs17\Apache24\bin
   ```

2. 然后输入以下命令进行安装

   ```shell
   httpd.exe -k install
   ```

3. 之后会出现防火墙设置，点击运行就行，然后出现下面提示就表示安装成功；

   ![image-20230808230739212](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230808230739212.png)

## 四、启动Apache

1. 在**bin**目录下找到**ApacheMonitor.exe**文件，双击启动；

   ![image-20230808230923054](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230808230923054.png)
   
2. **右键**图标，点击**Open Apache Monitor**打开窗口；

   ![image-20230808231020314](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230808231020314.png)

   ![image-20230808231053204](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230808231053204.png)

3. 点击**Start**，当亮起**绿灯**即表示启动成功；

   ![image-20230808231209417](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230808231209417.png)

4. 在网页上输入**localhost**，进入这个页面表示已经成功加载了；

   ![image-20230808232129267](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230808232129267.png)

5. 然后输入**localhost:81**（刚才确定的端口），就能进入到我们刚才自定义的文件目录了；

   ![image-20230808234036339](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230808234036339.png)

   ![image-20230808232341439](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230808232341439.png)

## 五、服务器设置

​	在服务器的防火墙规则上添加刚才定义的端口，既能通过**服务器的公网ip:端口号**访问资源文件，进而实现资源文件的下载；

![image-20230808232730551](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230808232730551.png)

## 参考资料

1. 云服务器上搭建Apache https://blog.csdn.net/weixin_45616775/article/details/109550217

