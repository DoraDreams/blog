title: phpmyadmin修改上传文件的上上限
date: 2016-05-24 15:37:34
tags:
---

## 方法

找到php.ini 我的是在/ect/php5/cgi/php.ini
修改
upload_max_filesize = 50M
 post_max_size = 50M

