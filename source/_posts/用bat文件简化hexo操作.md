---
title: 用bat文件简化hexo操作
date: 2018-07-09 23:50:11
tags: [hexo,bat,偷懒]
---
我也算是懒到一定境界了，连三行命令都不想敲了_(:з」∠)
<!--more-->
把下面的写到记事本里，保存并把后缀名改为.bat，写完博客双击一下这个文件就能完成“清空缓存，生成文件，部署”三连了。  
ps：显然我的本地博客路径是F:\Node_js_blog，用的时候把第一行的f:和第二行的路径根据自己情况自行更改即可。
```
f:
cd \Node_js_blog
call hexo clean
call hexo g
call hexo d
cd \
```
<!--more-->