title: java使用外来的jar包
date: 2016-03-18 19:56:15
categories: java
---
  这篇文章说明如何使用javac和java命令使用外部的jar包
  
  ## Linux
  在linux系统下使用的编译命令为:javac -classpath xxx.jar xyz.classpath
  java运行命令为: java -classpath xxx.jar: xyz  (这个冒号很重要，没有会提示找不到main class)
  
  ## windows
  在windows的使用的javac命令相同，只要把java的冒号改为分号即可
  
  ## issue
  很多人都会疑惑eclipse链接外部包时可以运行，但是自己却无法运行，问题就出在这个地方。而且在windows下，eclipse使用的是javaw命令，这个可以通过debug追踪线程查看到