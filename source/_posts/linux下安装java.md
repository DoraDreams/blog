title: linux下安装java
date: 2016-03-27 18:04:25
categories: linux, java
tags: [linux, java]
---
 这篇博文记录了linux下如何安装java 
 
 ##1.下载jdk
 前往orcale的官网下载jdk的安装包，一般为tar的压缩包
 
 ##2.解压jdk
 使用命令tar -zvxf xxxx
 
 ##3.移动和配置 将解压后的文件移动到你想要存放的位置，在这里笔者使用的文件夹为/usr/lib/jvm/jdk1.8（你可以选择自己喜欢的地方放置该文件）。接着修改/etc/profile 或者 ~/.bashrc (如果修改的是前者，需要使用命令source /etc/profile使其生效)。
 在其最后面加入几行语句 <br />
 export JAVA_HOME=/usr/lib/jvm/jdk1.8
 export JRE_HOME=$JAVA_HOME/jre
 export CLASSPATH=$CLASSPATH:$JAVA_HOME/lib:$JRE_HOME/lib
 export PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
 
 有些时候在变量前加上{}（${JAVA_HOME}也有这种写法的
 
 如果安装过程中出现了bash: /usr/lib/jvm/jdk1.8/bin/java: /lib/ld-linux.so.2: bad ELF interpreter: 没有那个文件或目录  是因为安装的位数和你操作系统的位数不匹配所导致的
 
 
