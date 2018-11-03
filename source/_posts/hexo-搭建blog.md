title: hexo 搭建blog
date: 2015-11-11 21:39:06
categories: hexo
tags: [博客， 文章]
---
 这是我第一个使用hexo搭建的blog，在这期间我也遇到了不少的问题， 现在将这些总结下。以后我也可以回忆。
 
 
## 步骤
### 1.github的安装
下载git，通过命令


 ``` bash 
$git ssh-keygen -t rsa -C "examplame@email.com"   examplame@email是你的邮箱
```

生成ssh key, 接着在github上添加ssh key， 同
时确保github上有以yourname.github.io命名的项目， 这时可以使用

 ``` bash 
$ ssh -T git@github.com 
```

进行测试。
	
###  2.node.js和hexo的安装
下载安装node.js， 打开git bash， 通过命令
		
``` bash 
$ npm install hexo -g  
```
		
安装hexo, 如果遇到
		
 ``` bash 
$ ERROR Deployer not found 
```

可以使用命令
		
``` bash 
$ npm install hexo-deployer-git --save 
```

###  3.blog目录的初始化

 ``` bash 
$ hexo init  //初始化目录
$ npm install  //安装依赖包
$ hexo g  //生成public目录下的文件
$ hexo s  //本地服务器浏览
```
		
###  4.部署到github上
在_congig.yml文件里找的deploy，增加以下几行(注意空格)
		
 ``` bash 
type: git
repository: it@github.com:yourname/yourname.github.io.git
branch: master 
```
		
输入hexo d -g部署
		
###  5.使用主题
到现在为止，你已经拥有一个yourname.github.io的blog了
我们可以对blog进行美化，使用一些现有的主题可以节省时间
使用get clone可以克隆主题
		
 ``` bash 
$ hexo new page "ex" //可以生成新页面
$ hexo new ""  //生成新文章

hexo clean // 清楚缓存
hexo g = hexo generate // 生成网页
hexo d = hexo deploy  // 部署到github上
```

如果要绑定域名，可以再source下创建CNAME， 在CNAME中写上你要绑定的域名
比如说fangxuan.win
或者可以在项目的setting中，有个custorm domain 里面也可以填写上你的域名
		
更多的自己研究吧 O(∩_∩)O哈！
