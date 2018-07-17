---
title: JavaDoc语法
date: 2018-07-07 15:15:09
tags: [Java,纯记忆的学习笔记]
preview: https://raw.githubusercontent.com/Laurence-042/Resources/master/jpg/anim/yande.re%20366931%20ram_(re_zero)%20rem_(re_zero).jpg
---
文档要好好写哦！（小声：然而我也不愿意写······）
<!--more-->

|标签|描述|示例|
|:---|:---|:---|
|@author|标识一个类的作者|@author description|
|@deprecated|指名一个过期的类或成员|@deprecated description|
|{@docRoot}|指明当前文档根目录的路径|Directory Path|
|@exception|标志一个类抛出的异常|@exception exception-name explanation|
|{@inheritDoc}|从直接父类继承的注释|Inherits a comment from the immediate surperclass.|
|{@link}|插入一个到另一个主题的链接|{@link name text}|
|{@linkplain}|插入一个到另一个主题的链接，但是该链接显示纯文本字体|Inserts an in-line link to another topic.|
|@param|说明一个方法的参数|@param parameter-name explanation|
|@return|说明返回值类型|@return explanation|
|@see|指定一个到另一个主题的链接|@see anchor|
|@serial|说明一个序列化属性|@serial description|
|@serialData|说明通过writeObject( ) 和 writeExternal( )方法写的数据|@serialData description|
|@serialField|说明一个ObjectStreamField组件|@serialField name type description|
|@since|标记当引入一个特定的变化时|@since release|
|@throws|和 @exception标签一样.|The @throws tag has the same meaning as the @exception tag.|
|{@value}|显示常量的值，该常量必须是static属性。|Displays the value of a constant, which must be a static field.|
|@version|指定类的版本|@version info|
<!--more-->