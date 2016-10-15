# GitHub && Git 使用记录 #
## 什么是GitHub ##
> 每当了解一个新玩意的时候首先我想知道的总是这玩意到底是个啥。GitHub嘛，不就是为开发者提供 Git 仓库的托管服务嘛，同时你可以分享你的仓库给任何人，通俗来说，大致上就像一个可以查文件修改历史的网盘。你可以不断得提交你修改的文件（这里的文件可以是你写的小说啊，你制作的视频啊，你偷藏的电子书啊，还可以是你辛辛苦苦抹的代码），同时可以恢复到旧的版本。还可以邀请其他人来和你一起改你的文件。差不多就是这么个简单的玩意儿。当然，在你了解了之后会发现，他还有很多666的功能。OK，我来附上[**官方网址**](https://github.com/)，大家可以先看看这哥们的样子。另外这里有GitHub被玩坏的[**LOGO**](https://octodex.github.com/)。

## 什么是Git ##
> Git 属于分散型版本管理系统，是为版本管理而设计的软件。它是由Linux 的创始人 Linus Torvalds 在 2005 年开发了的原型程序发展而来。其性能和功能自然没的说，用过的基佬都说好~

## 注册使用GitHub ##
> 去[**官方网址**](https://github.com/)注册就好了没啥特别说明的地方。注册之后包括仓库、分支的创建等官方都给出了[**图文教程**](https://guides.github.com/activities/hello-world/)，这里不再赘述。虽然是英文版的，但是希望大家能耐着性子看看（已经熟悉的同学可以直接忽略），更多[**官方教程**](https://guides.github.com/)可以看这里。

## 安装Git ##
> 扯了半天没用的，赶紧进入正题，要想使用GitHub，首先我们需要安装Git，MAC和linux系统不必多说了，一般现在的系统都是默认安装Git，我就只说一下windows的安装，首先当然是下载[**Git for windows**](http://msysgit.github.io/)([或者从这里下载也可以](https://git-scm.com/downloads/)),下载完成后安装，这里对几个安装选项进行简单的说明，配置好一路next，最后点击install就完成安装了（下图是我在安装时勾选的选项）。

![安装步骤1](/Code/Img/Git/git_install1.jpg)
![安装步骤2](/Code/Img/Git/git_install2.jpg)
![安装步骤3](/Code/Img/Git/git_install3.jpg)
![安装步骤4](/Code/Img/Git/git_install4.jpg)
![安装步骤5](/Code/Img/Git/git_install5.jpg)

## 使用Git ##
#### 初始设置 ####
> 设置姓名和邮箱（该设置会在**~/.gitconfig**中生成配置，并且在提交时会被公开哦~）：
```
//设置姓名
git config --global user.name "L.T.Any"
//设置邮箱
git config --global user.email "linetoanywhere@gmail.com"
//设置输出内容高亮
git config --global color.ui auto
```

#### 设置SSH Key ####
> 使用GitHub连接到已有仓库时，需要使用SSH的公钥进行认证，因此我们需要在本地创建一对密钥，本地Git Bash上执行如下：  
![生成SSH Key](/Code/Img/Git/SSH_Key.gif)  
创建好SSH Key后，我们需要把它导入到GitHub中去，具体导入过程见下图：  
![导入SSH Key](/Code/Img/Git/add_ssh_key.png)  
导入完成后我们可以简单测试一下是否可用，具体检验方法如下：（当出现Hi 。。。。 access这样的输出时说明可用）  
![检验SSH Key](/Code/Img/Git/check_ssh_key.png)  
至此，SSH Key设置完成。

#### 下载代码仓库 ####
> 创建好代码仓库后就可以将他们下载到本地来进行编辑修改了。在GitHub上进入仓库页，选择**Clone or Download**，这里可以选择使用https或者SSH，由于我们设置了SSH，因此选择SSH，复制地址。  
![检验SSH Key](/Code/Img/Git/Clone_Or_Download.png)
```
//克隆仓库内容到本地
git clone git@github.com:LineToAnyWhere/LineToAnyWhere.github.io.git
```
