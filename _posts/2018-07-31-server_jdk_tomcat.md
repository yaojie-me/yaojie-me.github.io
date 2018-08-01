---
layout: post
title: CentOS 7 部署 JDK 1.8 和 Tomcat 8
categories: Server
description: CentOS 7 部署 JDK 1.8 和 Tomcat 8
keywords: CentOS, JDK, Tomcat
---


## Linux 服务器部署 JDK 1.8 和 Tomcat 8

网上有很多教程都是教用户部署 JDK 和 Tomcat 的，但是介绍的都很简单，往往无法满足我们对于企业用户的需求。


### JDK 1.8 下载、安装

1,切换到安装目录
```
cd /usr/local/
```
2,下载安装文件（这个链接无法直接使用，对应的 AuthParam 信息需要动态生成，所以你需要去官网自行查找下载链接）
```
sudo wget http://download.oracle.com/otn-pub/java/jdk/8u181-b13/96a7b8442fe848ef90c96a2fad6ed6d1/jdk-8u181-linux-x64.tar.gz?
AuthParam=1533007873_0a7882571ae7718f3ab0795c4b257277
```

3,重命名刚才下载的文件
```
mv jdk-8u181-linux-x64.tar.gz\?AuthParam\=1533007873_0a7882571ae7718f3ab0795c4b257277 jdk-8u181-linux-x64.tar.gz
```

4,解压
```
tar -zxvf jdk-8u181-linux-x64.tar.gz
```

5,删除刚才下载的源文件
```
rm -rf jdk-8u181-linux-x64.tar.gz
```

6,配置超链接指向刚才安装的 JDK，这样以后修改 JDK 版本、位置的时候不用修改其他配置
```
ln -s jdk1.8.0_181 jdk
```

7,设置环境变量
```
vim + /etc/profile
```

8,添加环境变量
```
JAVA_HOME=/usr/local/jdk
PATH=$JAVA_HOME/bin:$PATH
CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export JAVA_HOME
export PATH
export CLASSPATH
```

9,使修改生效
```
source /etc/profile
```

10,查看 PATH
```
echo $PATH
```

11,检查安装是否成功
```
java -version
```

### Tomcat 8.5 下载、安装

1,切换到安装目录
```
cd /usr/local/
```

2,下载源文件
```
sudo wget https://mirrors.tuna.tsinghua.edu.cn/apache/tomcat/tomcat-8/v8.5.31/bin/apache-tomcat-8.5.31.tar.gz
```

3,解压
```
sudo tar -zxvf apache-tomcat-8.5.31.tar.gz
```

4,删除源文件
```
sudo rm -rf apache-tomcat-8.5.31.tar.gz
```

5,配置超链接
```
sudo ln -s apache-tomcat-8.5.31 tomcat
```

6,设置环境变量
```
sudo vim + /etc/profile
```

7,添加环境变量
```
export CATALINA_HOME=/usr/local/tomcat
```

8,使修改生效
```
source /etc/profile
```

9,赋予用户读取执行权限
```
sudo chmod -R a+rx *
```


### 结束语
至此，JDK 和 Tomcat 的安装都已完成，二者的安装方式类似，都是使用创造超链接的方式，避免其修改是，影响其他配置。
后续章节，我们会继续学习其他组件，例如 Jenkins，Gitlab，等的安装和配置，最终搭建一个自动部署系统。