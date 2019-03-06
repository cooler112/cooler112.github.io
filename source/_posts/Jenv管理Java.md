---
title: Jenv管理Java
date: 2019-03-06 17:30:12
tags: 编程工具
---

什么是Jenv：http://jenv.io/ 
jenv is Java environment manager, and it is a clone of RVM for Java. jenv can manage parallel versions of Java development kits on any Unix based system. It provides a convenient command line interface for installing, switching, removing and listing Candidates.

也就是各类JAVA环境的安装配置，如果手工去作是一件很麻烦的事情，但是有了这个工具后，简单命令即可实现快速配置。


Why jenv？
* Easy to manage Java version, such as 1.6, 1.7, 1.8 and 1.9
* Easy to install Java tools, such as Ant, Maven, Tomcat etc.
* Easy to manage candidate's version such as install new version or uninstall the old one.
* Directory is standard, and friendly to IDE
* Easy to extend. You can setup your own jenv on your company to manage development environment.
* Easy to backup your env.
* Bash completion support. Use TAB to complete command name, candidate name and version.
  为什么使用呢？很清楚
  方便切换JDK环境，方便安装各类Java工具
  方便更新包管理，界面友好、方便拓展备份、自动命令行补充等等

下载步骤：
$ curl -L -s get.jenv.io | bash

$ mkdir -p $HOME/.jenv/candidates/java

配置Java环境：
从官网下载各类JAVA的JDK：
http://www.oracle.com/technetwork/java/javase/downloads/index.html
安装后添加链接：
ln -s /Library/Java/JavaVirtualMachines/jdk1.8.0_151.jdk/Contents/Home ~/.jenv/candidates/java/1.8.0_151
启用该环境
Jenv default java 1.8.0_151 即可

安装第三方如Maven 
$ jenv list maven
Final install the candidate with the version:
$ jenv install maven 3.3.9
In your terminal, input mvn --version to check the installation.

通过jenv -h可以知道很多常用的命令
可以使用jenv all查看所有支持的第三方

灵活的安装方式
Install candidates in other ways
Install from local folder:
$ jenv install java 1.8.0_71 /user/local/jdk-1.8.0_71
Install from git repository:
 ​$ jenv install spike 0.0.1 git@github.com:linux-china/groovy_scripts.git

方便的更新
How to sync candidates information with the repository
jenv stores the repository information with offline mode, please use following command to update repository information.
$ jenv repo update

How to update jenv
Please use selfupdate command to get last version.
$ jenv selfupdate

jenvrc support
jenvrc is jenv setup file which contains candidate and the version as following:
java=1.8.0_71
maven=3.3.9
After you enter this directory, jenv will setup environment automatically.