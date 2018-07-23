---
title: 用bat文件简化hexo操作
date: 2018-07-09 23:50:11
tags: [hexo,bat,偷懒]
---
我也算是懒到一定境界了，连三行命令都不想敲了_(:з」∠)
<!--more-->
### 自动清空缓存，生成文件，部署
把下面的写到记事本里，保存并把后缀名改为.bat，写完博客双击一下这个文件就能完成“清空缓存，生成文件，部署”三连了。  
ps：显然我的本地博客路径是F:\Node_js_blog，用的时候把第一行的f:和第二行的路径根据自己情况自行更改即可。
```shell
@echo off
f:
cd \Node_js_blog
call hexo clean
call hexo g
call hexo d
cd \
```
注：我写给自己用的.bat在`call hexo g`和`call hexo d`之间还有一行`copy /y F:\Node_js_blog\source\google31436e429f369257.html F:\Node_js_blog\public\google31436e429f369257.html`，用于将public文件夹下的那个文件替换为source文件夹里文件。那个文件是Google的验证文件，把这个文件原样上传到服务器是Google用来验证我的博客的确是属于我的方法。但hexo d会把它以博文的形式进行修改，所以在我找时间学会hexo主题的写法之前只能加这一步把它替换回来了
### 自动创建新博客文章并用编辑器打开
把下面的写到记事本里，保存并把后缀名改为.bat。hexo new 输完文章标题还要去文件管理器找_post文件夹并找到文章双击简直太麻烦了（旁白：是你太懒了吧喂！），所以就有了这个  
ps：显然我的本地博客路径是F:\Node_js_blog，准备用VS Code打开，而且我的VS Code安装在了D:\Microsoft VS Code，用的时候把第一行的f:和第二行的路径以及编辑器可执行文件的路径根据自己情况自行更改即可。
```shell
@echo off
f:
cd \Node_js_blog
set /p name=请输入文章名字：
echo 输入的是: %name%
echo 请等待······
@echo A|call hexo new "%name%"
echo 请等待······
start /d "D:\Microsoft VS Code"   Code.exe  "F:\Node_js_blog\source\_posts\%name%.md"
```
<!--more-->