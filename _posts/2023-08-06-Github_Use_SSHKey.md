---
layout: post
title: "Github使用ssh key"
date:   2023-08-04
tags: [Github]
comments: true
author: Mroach-233
---

之前一直把TortoiseSVN跟Gitee结合来使用，在电脑的本地凭据上保存有数据，每次提交代码的时候都比较方便，最近在Github上也部署了些项目，发现提交的时候会有些问题，不支持密码验证了。网上搜了搜，有说使用**个人访问令牌**的，但是在github上找半天也没找着，我看网上用的比较多的是用**ssh key**，这里记录下使用过程。

<!-- more -->

## 第一步

在Git的安装目录下找到**git-bash.exe**这个文件，然后打开它；

<img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230804202326759.png" alt="image-20230804202326759" style="zoom:80%;" />





接着依次输入以下命令：

```
cd ~/.ssh
```

```
ls
```

第一个命令是寻找电脑目录里带.ssh文件夹的，第二个命令是查看文件列表的；

如果能找到下图的两个文件的话，可以跳过第二步；

![image-20230804202938681](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230804202938681.png)

## 第二步

如果在上述步骤中没有找到，那就要创建ssh key了，输入以下命令：

```
ssh-keygen -t rsa -C "xxx@xxxx.com"
```

`xxx@xxxx.com` 为github的注册邮箱，然后一直回车确认，就生成好了；

<img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230804215044060.png" alt="image-20230804215044060" style="zoom:80%;" />



## 第三步

接着打开文件生成的路径，之前生成的时候有提示，一般是"**C:\Users\xxxx\\.ssh**"，这两个就是生成的文件了；

<img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230804220306276.png" alt="image-20230804220306276"  />

右键使用记事本打开**id_rsa.pub**文件，打开里面大概像这样，然后复制里面的内容；

![image-20230804220444133](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230804220444133.png)

接着打开github绑定公钥，点击**右上角的头像**，点击**Settings**;

<img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230804221152583.png" alt="image-20230804221152583" style="zoom:67%;" />

然后在左侧点击**SSH and GPG keys**；

<img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230804221314695.png" alt="image-20230804221314695" style="zoom:80%;" />

然后点击右上角的**New SSH key**;

<img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230804221419096.png" alt="image-20230804221419096" style="zoom:80%;" />

在**Key**里粘贴刚才**id_rsa.pub**里复制的内容，Title可以随便填，然后点击**Add SSH key**;

<img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230804221706520.png" alt="image-20230804221706520" style="zoom: 67%;" />

## 第四步

这时候可以进行验证，输出以下命令：

```
ssh -T git@github.com
```

如果如下图所示，则说明设置成功了，之后就能通过SSH来克隆或者提交项目了；

<img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230804224135905.png" alt="image-20230804224135905" style="zoom:80%;" />

<img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230804222012202.png" alt="image-20230804222012202" style="zoom:80%;" />

如果没有验证成功可能是因为没有识别到公钥，可以输入以下命令：

```
ssh-add ~/.ssh/id_rsa
```

如果出现报错"**Error connecting to agent: No such file or directory**"，可以**管理员身份**打开**Windows PowerShell** ，输入以下命令检查ssh-agent服务是否启动成功：

```
get-service ssh*
```

![image-20230804232139585](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230804232139585.png)

如果发现ssh-agent状态为stopped，则依次输入以下命令：

```
Set-Service -Name ssh-agent -StartupType Manual
```

```
Start-Service ssh-agent
```

然后再次执行**get-service ssh***命令，发现ssh-agent服务正在运行就没问题了；

![image-20230804232448482](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230804232448482.png)

然后回到之前的页面，再次验证就没问题了。



## 一些小问题

1. 有时候本地的项目是之前用https克隆的，懒得重新使用SSH克隆的话，可以在项目所在目录下的**.git文件夹**里找到**config**配置文件；

   <img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230806021605762.png" alt="image-20230806021605762" style="zoom:67%;" />

记事本打开后将原来的**url地址**换成SSH的即可；

<img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230804222619842.png" alt="image-20230804222619842" style="zoom:80%;" />

2. 我本地使用的是TortoiseGit，克隆项目到本地的时候会出现以下错误：

![image-20230804232737879](https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230804232737879.png)

可以依次选择：鼠标右键->TortoiseGit->Settings->Network，修改SSH client路径；

<img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230804233046275.png" alt="image-20230804233046275" style="zoom:67%;" />

选择Git安装目录下的**/usr/bin/ssh.exe**，然后应用即可；

<img src="https://raw.githubusercontent.com/Mroach-233/Mroach-233.github.io/master/images/image-20230804233211440.png" alt="image-20230804233211440" style="zoom:67%;" />

