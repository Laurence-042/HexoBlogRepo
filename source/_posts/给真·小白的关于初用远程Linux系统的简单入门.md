---
title: 给真·小白的关于初用远程Linux系统的简单入门
date: 2018-08-08 14:17:20
tags: [真·小白, Linux]
---
真的是给真·小白的入门教程，详细到几乎每一条命令都有一个截图,结果就是······图很多，流量慎入
<!--more-->

本教程专门面向小白写成，提到的命令都是最常用而且最简单的版本（比如单一个“下载”就有下载到当前目录，下载到指定目录，速度限制等一堆可选项，这里只会提及“下载到当前目录”这个最简单的版本。  

### 1. 初次连接
打开Xshell后会出现这个这个界面，第一次连接的话需要新建连接配置，点击“新建”即可
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/00.JPG)

你首先会看到这个界面，虽然设置很多，但对初学者来说只要填两个地方就行了：IP和用户信息
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/01.JPG)

填写服务器IP（租服务器时服务器提供商会告诉你的）
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/02.JPG)

填写用户名和密码（root用户的话，服务器提供商会告诉你，其他用户由root用户创建，问root用户要用户名和密码）
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/03.JPG)
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/04.JPG)

填好后按“确定”就能看到新建的连接配置了
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/05.JPG)

双击这个配置或选中后点“连接”即可连接服务器（如果网络没问题而且也没有因为某些众人皆知的原因连不上服务器的话）  
连接后你会看到类似这样的界面，这就代表连接成功了
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/06.JPG)

### 2. 工作目录的切换

“工作目录”其实也就是我们常说的“文件夹”，切换工作目录也就相当于打开/关闭文件夹  

#### 2.1: ls
`ls`：最常用的命令，输入ls后按回车即可查看这个文件夹下的所有文件的名字
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/07.JPG)

#### 2.2: pwd
`pwd`：查看目前工作目录的绝对路径（迷路真的是很糟糕的体验）下图中输出的`/home/hentai`就表示现在打开的文件夹是根目录`/`下的`home`文件夹中的`hentai`文件夹
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/08.JPG)

#### 2.3: cd
`cd`：进入目录，也就是“打开文件夹”  
格式为`cd [想打开的文件夹的路径]`  
这个例子里，`[想打开的文件夹的路径]`就是`TestFile`  文件夹
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/09.JPG)

“路径”有“相对路径”和“绝对路径”之分，比如刚刚的情况下，我们已打开的文件夹的绝对路径就是`/home/hentai`，想要打开的文件夹的绝对路径是`/home/hentai/TestFile`，那么TestFile文件夹对hentai文件夹的相对路径就是`TestFile`
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/10.JPG)

若想回到上级目录（前一个文件夹），输入`cd ..`即可，此处可以认为`..`代表的就是上级目录的路径
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/11.JPG)

`cd`命令后面不仅可以用相对路径，也可以用绝对路径，比如下图这样的，就是用了绝对路径进入了`hentai`目录的上级目录`home`
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/12.JPG)

再用绝对路径进入`hentai`目录
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/13.JPG)

#### 2.4: vi
`vi`：利用名字是“vi编辑器”编辑文件  
在Linux系统中，vi编辑器的进阶版本也就是vim编辑器因其强大的功能与可定制性而出名，但不是所有系统初始就带着vim，但一般都带着vi。在简单使用时vi和vim的操作几乎完全相同
格式为`vi [试图打开的文件的路径]`，相对路径 和绝对路径都可以  
就像刚刚说`cd`时提到的，本目录下的文件的`[试图打开的文件的路径]`也就是文件名  
在下图的例子中，就是用vi打开文件`README.html`
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/14.JPG)

*注：你可能会看到这个界面，这是因为可能有其他人刚刚编辑过/正在编辑这个文件。但如果你是自己一个人用这个服务器，基本不太可能出现这种情况*
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/15.JPG)

这是打开后的界面，可以用方向键移动光标（也就是下图中绿色的东西），按`i`键可进入插入模式，在这个模式下，你可以编辑一个文件（比如往里面加字或删字）
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/16.JPG)

加了几个字······  
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/17.JPG)

按`Esc`键推出插入模式  
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/18.JPG)

然后输入`:wq`保存并推出文件  
注意，冒号是英文的半角冒号。  
`:wq`这三个字符分别代表“选项”“写入”和“退出”，连在一起也就是“保存并退出”，你可能意识到了，顺手保存一下不退出就是`:w`，如果想不保存强制退出，就`:q!`（`!`代表“强制”）  
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/19.JPG)
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/20.JPG)

如果`vi [试图打开的文件的路径]`中`[试图打开的文件的路径]`并不存在，那么写入内容并保存的话就会新建这个文件  
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/21.JPG)
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/22.JPG)
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/23.JPG)

#### 2.5: rm
`rm`：删除文件  
格式为`rm [选项] [想删除的文件路径]`，`[选项]`非必须  
比如下图中，`[选项]`就是`-f`，代表强制删除 
如果没有这个，直接`rm Test-vi`的话，系统会询问你是否确定要删除，输yes确认删除  
（不要介意下方的那个黄色图标，那是我的一个桌面插件在提醒我有新邮件）  
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/24.JPG)

你也可以用`rm`删除目录（文件夹），这时候`[选项]`中要有`-r`代表“递归删除”也就是删除这个文件夹和其中的所有东西，  
下图的例子中同时启用了两个选项“强制删除”和“删除文件夹”  
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/25.JPG)

值得一提的是，你只能删除对你开说“可写”的文件，如果你没有对这个文件“写”的权限，你是无法删除它的。  
使用`ls -l`即可查看文件的详细信息。左侧的`rwx`分别代表“可读”“可写”“可执行”，`-`代表“无权”。三组rwx分别代表“此用户”“同组用户”“其他用户”对这个文件的权限。  
以下图的`Test-File.jpg`为例，用户hentai可以读写这个文件（可以打开看，可以编辑删除），用户组hentai中的其他用户只能读这个文件（可以打开看，但不可以编辑和删除）
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/26.JPG)

#### 2.6: wget
`wget`：从互联网上下载文件  
格式为`wget [下载链接]`  
下图的示例就是用`sao_utils_beta1_update2.1.exe`对的下载链接下载这个文件
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/27.JPG)
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/28.JPG)

#### 2.6: rz

**注意：这个功能并非Linux服务器标配，如果该命令无效，需要先输`yum  install lrzsz`安装`lrzsz`后才能使用**

`rz`：从本地上传文件  
格式为`rz`，输入后点击回车就会弹出选择本地文件的窗口，选择后即可开始上传  
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/29.JPG) 
![](https://raw.githubusercontent.com/Laurence-042/Resources/master/post/%E7%BB%99%E7%9C%9F%C2%B7%E5%B0%8F%E7%99%BD%E7%9A%84%E5%85%B3%E4%BA%8E%E5%88%9D%E7%94%A8Linux%E7%B3%BB%E7%BB%9F%E7%9A%84%E7%AE%80%E5%8D%95%E5%85%A5%E9%97%A8/30.JPG)

#### 2.7: sz

**注意：这个功能并非Linux服务器标配，如果该命令无效，需要先输`yum  install lrzsz`安装`lrzsz`后才能使用**

`sz`：从下载文件到本地  
格式为`sz [想下载的文件路径]`，输入后点击回车就会弹出选择下载位置的窗口，选择后即可开始下载  
由于和`rz`使用极度相似，就不配图了

---

教程到这里就结束了，祝你在Linux服务器上玩得开心（笑）

<!--more-->
