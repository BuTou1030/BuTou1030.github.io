---
title: 搭建hexo博客遇到的问题
copyright: true
date: 2021-03-04 19:14:41
toc: true
tags: [问题,博客]
categories: [问题,博客]
---
在搭建hexo个人博客的部署环节
<!-- more -->
对于上传不了博文的解决方案

博文顶部配置属性冒号后面要有空格!

我的做法是：
1、先把git加入系统环境变量；
2、再将博客目录里的.git文件夹删除
3.、命令步骤：
   hexo clean
1
   hexo  g
1
   hexo  d
1
4、至此，解决
建议：不要使用cmd上传，用Git bash或其他
+

最后放上我的报错截图：

————————————————![img](https://img-blog.csdnimg.cn/20190404135506907.PNG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L25qY19zZWM=,size_16,color_FFFFFF,t_70)
版权声明：本文为CSDN博主「摘星星的Q」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/njc_sec/article/details/89021083