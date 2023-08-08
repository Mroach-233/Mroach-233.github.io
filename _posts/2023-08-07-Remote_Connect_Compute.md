---
layout: post
title: "远程连接家里电脑"
date:   2023-08-07
tags: [远程桌面连接]
comments: true
author: Mroach-233
---

最近有个需求是要**在公司远程家里的电脑**码代码（可能有人会说，在公司电脑上git一下不就好了，emmmm公司的环境比较复杂，不太好搞，而且有监听），向日葵、ToDesk这类软件也能远程电脑，但是画质，延迟啥的懂得就懂。因为家里的电脑没有公网IP，网上搜了下，可以通过云服务做**内网穿透**，恰巧手上就有一个闲置的服务器，开搞！

<!-- more -->

## 前提准备

### 设备：

公司的电脑（带远程桌面连接）

云服务器（带公网ip，系统是**Windows server**）

客户端（家里的电脑，能连网，带远程桌面连接）

### 软件：

**Frp**，内网穿透：https://github.com/fatedier/frp/tags

**Winsw**，让软件变成系统服务：https://github.com/winsw/winsw/tags

## 客户端

1. 下载Frp，注意下载的是“**frp_0.51.2_windows_amd64.zip**”，不要下错了，是带**amd**的，不是**arm**；

   ![image-20230807172540250](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230807172540250.png)

   解压之后文件内的目录结构大致长这样，其中上面带'**c**'的是用于客户端，'**s**'的则是用于服务器上的。也就是说客户端上的可以把用于服务器上的三个文件给删了，服务器同理。

   ![image-20230807173520921](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230807173520921.png)

2. 用记事本打开**frpc.ini**文件，可以看到以下内容，**server_addr**填的是服务器的公网ip，**server_port** 设置的是服务器使用的端口，例如是9801，**local_port** 则是本机的端口，例如3389，而**remote_port** 则是远程桌面访问的端口，例如9800，之后就可以通过**服务器公网ip:9800**来进行远程访问；

   ![image-20230807174323408](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230807174323408.png)

3. 下载**Winsw**，根据系统选择下载64位的还是32位的文件，下载到Frpc文件里，并重命名为**frpclient.exe**（自定义），并创建同名的.xml文件，如**frpclient.xml**;

   ![image-20230807192840731](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230807192840731.png)

   ![image-20230807193159512](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230807193159512.png)

4. 记事本打开**frpclient.xml**文件，并输入以下配置信息：

   ```xml
   <service>
   	<id>frpClient</id>
   	<name>frpClient</name>
   	<description>内网穿透客户端</description>
   	<executable>%BASE%\frpc.exe</executable>
   	<arguments>-c %BASE%\frpc.ini</arguments>
   </service>
   ```

5. 命令行打开到该文件的根目录，然后输入以下命令：

   ```shell
   .\frpclient.exe install
   ```

6. **Win+S**搜索**服务**，在里面找到**frpclient**，并右键启动；**Win+S**搜索**服务**，在里面找到**frpclient**，并右键启动；

   ![image-20230807193833427](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230807193833427.png)

7. **Win+S**搜索**远程桌面设置**，然后打开；

![image-20230807202353976](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230807202353976.png)

## 服务器

1. 登录云服务器，同样下载**Frp**，只不过这次修改的是用于服务器的文件，打开**frps.ini**，修改配置信息，将**bind_port**改为与**server_port**对应的端口号；

   ![image-20230807202456136](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230807202456136.png)

2. 同样下载**Winsw**到该目录下，并重命名为**frpserver.exe**（自定义），也同样建立同名的.xml文件，如**frpserver.xml**，并输入以下配置信息：

   ```xml
   <service>
       <id>frpServer</id>
       <name>frpServer</name>
       <description>内网穿透服务端</description>
       <executable>%BASE%\frps.exe</executable>
       <arguments>-c %BASE%\frps.ini</arguments>
   </service>
   ```

3. 同样在命令行（管理员权限）中打开到该目录，然后执行以下命令，并启动该服务；

   ```shell
   .\frpserver.exe install
   ```

4. 在云服务器上设置防火墙规则，并添加刚才在客户端**frpc.ini**文件中配置的**server_port** 和**remote_port** 这两个端口号；

   ![image-20230807194610976](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230807194610976.png)

   ![image-20230807194642166](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230807194642166.png)

   

之后在公司的电脑上打开**远程桌面连接**，输入**服务器公网ip:remote_port**，再输入家里电脑开机时的账号密码即可。

## 一些问题

1. 电脑没有**远程桌面连接**，可以在系统里看看电脑是不是**专业版**，家庭版是没有远程桌面连接这个功能的，可以在万能的某宝上面搞一个激活码，也就两三块钱的事；

   ![image-20230807200653946](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230807200653946.png)

## 参考资料

1. windows server 部署frp内网穿透，并添加为服务 https://blog.csdn.net/qq_34361311/article/details/123079200