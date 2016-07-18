---
title: mysql5.7安装的诸多问题
date: 2016-07-18 12:53:00
categories: 教程
tags: [mysql,工具]
---
>今天在安装mysql5.7的时候遇到很多问题，原以为简单的下载安装即可了事，却废了大半天功夫，所以写这篇博客记录一下，也给遇到同样问题的朋友一点指引。

><!--more-->

#下载

在这里我下载的是windows64位5.7免安装版
![](/images/mysql-5.7-install/mysql-install-1.png)


###安装mysql服务
解压即可，不过mysql的服务还是要手动进行安装。
在开始菜单点开的搜索框中输入cmd，会找到一个黑色框框的cmd程序，右键程序以管理员身份运行，如果不以管理员身份运行的话，会报错。
进入自己本地的mysql的安装路径下的bin目录(即刚刚的解压路径),在这里我的路径是F:\\mysql-5.7.13-winx64\\bin
![](/images/mysql-5.7-install/mysql-install-2.png)


接着在命令行中输入
`mysqld install`
注意是mysqld不是mysql
![](/images/mysql-5.7-install/mysql-install-3.png)

在这里因为我已经安装过了所以显示结果和你们不一样
这样mysql服务就安装完成了。确认mysql服务是否安装成功可以在系统服务打开查看，如果在系统服务列表中有mysql服务，则表明mysql服务安装完毕

![](/images/mysql-5.7-install/mysql-install-service.png)


###启动服务
接下来就是启动mysql的服务了，启动的时候只要在命令行敲如下命令即可

`net start mysql`

但是此时会出错，服务无法启动，那是因为我们还没做初始化动作。
在启动之前我们得先初始化，mysql5.7版本的发布是5.6版本后的巨大进步，当然这是废话，主要是在服务器使用mysql的速度效率都是杠杠的，还有对JSON的支持，要不然我也不会上来就使用5.7版本的，当然以上只是我的一点愚见，回到正题，mysql5.7和5.6在下载后的目录就有一定的区别的，所以不要以为只是性能其他方面的提升，首先data目录在5.7里面是没有的，心细的朋友肯定发现了，为什么没有了呢，其实我也不知道，对于初学者来说可以慢慢了解，我们主要来说明如何开启服务，首先使用初始化的命令就会生成data目录！如下是解决方案。

解决方案：
使用 mysqld  --initialize 进行初始化，就会出现data文件夹，但是你要注意生成的时候也会出错的，当然我也会告诉你怎么解决：在你的mysql目录下有一个my-default.ini的配置文件，在这新建一个my.ini(my.ini会自动覆盖my-default.ini)文件，文件内容如下

```

[mysql]

# 设置mysql客户端默认字符集

default-character-set=utf8 
[mysqld]
#设置3306端口
port = 3306 
# 设置mysql的安装目录
basedir=F:\mysql-5.7.13-winx64
# 设置mysql数据库的数据的存放目录
datadir=F:\mysql-5.7.13-winx64\data
# 允许最大连接数
max_connections=200
# 服务端使用的字符集默认为8比特编码的latin1字符集
character-set-server=utf8
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB 
```
不过其中的文件路径得改成自己的， 具体my.ini配置也可以去百度看看，大致都一样，可以自己去试试，干这行就得试！好了最后通过mysql  --initialize生成data文件夹你的服务就可以成功打开了！不过在初始化的时候你可能会遇到这个问题
![](/images/mysql-5.7-install/mysql-install-5.png)
大概意思是读取my.ini文件时出错。
那么这个问题又是该怎么解决呢，那是因为你在通过记事本或者其他编辑器以utf8编码保存上述my.ini文件的时候，编辑器自动给文件加上了utf8签名,
[什么是utf8签名](http://blog.csdn.net/linux7985/article/details/7663444)。好了，简单的来说就是文件开头有3个字节大小的的标识符，用来标识该文件是以utf-8来编码，从而来简化一些软件的解码过程，可在方便某些软件的同时也带来了许多麻烦，因为另一些软件并不认识utf8签名，这些软件会把标识符当做文件的内容来读取，从而导致错误，这里的mysql启动服务读取my.ini文件就不能识别utf8签名，所以会出现以上问题，解决方法可以用UltraEdit(一款编辑器,大家可以自行度娘)来打开我们的文件并另存为UTF-8(无BOM)格式,保存完后不要再以记事本打开编辑，因为编辑完再保存的时候，文件开头又会带上utf8签名，这时又得打开UltraEdit来重新另存为一下了，当然如果你有兴趣的话，可以看看这段utf8签名的‘真面目’,用UltraEdit打开文件，选择工具栏的编辑，再选择右边16进制模式,如果我们的文件此时是utf8签名的话，文件开头会是EF BB BF![](/images/mysql-5.7-install/mysql-install-4.png)。在解决了上述的问题之后,现在我们可以回到启动mysql服务了，在控制台输入
`net start mysql`

这时就会提示成功
```
Mysql 服务正在启动
Mysql 服务已经启动成功
```

###登录mysql服务器
在mysql5.6中,默认有户名是root,密码为空,但是5.7中的默认密码不是空,又是一大头疼事。

现在我们就来看看密码藏在哪,在mysql的安装目录下的data目录中有个以.err后缀结尾的文件
![](/images/mysql-5.7-install/mysql-install-6.png)

通过编辑器的查找功能,我们可以找到密码
![](/images/mysql-5.7-install/mysql-install-7.png)

下面就可以通过这个密码来进行登录了

`mysql -uroot -p******`
\*\*\*\*\*指的是在上述文件中找到的密码


![](/images/mysql-5.7-install/mysql-install-8.png)


到这里总算是结束了,没想到安装个mysql都这么费劲


[参考文章](http://bbs.csdn.net/topics/391902223?list=lz)



