# GitHub & Git 使用记录 #
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
> 设置姓名和邮箱（该设置会在** ~/.gitconfig **中生成配置，并且在提交时会被公开哦）：
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

#### 下载并使用代码仓库 ####
> 创建好代码仓库后就可以将他们下载到本地来进行编辑修改了。在GitHub上进入仓库页，选择**Clone or Download**，这里可以选择使用https或者SSH，由于我们设置了SSH，因此选择SSH，复制地址，打开git，切换到目标目录，并执行如下命令。  
![检验SSH Key](/Code/Img/Git/Clone_Or_Download.png)
```
//克隆仓库内容到本地
git clone git@github.com:LineToAnyWhere/LineToAnyWhere.github.io.git
```
> 此时仓库已经下载到本地，这时我们可以修改内容，然后在本地仓库中添加更改，之后提交更改。可以在内容更改后执行如下命令来在本地提交更改：
```
//添加更改后的文件到仓库中,当然也可以直接添加目录
git add xxx.html    //添加单个文件到目录
git add .           //添加当前目录中的文件
//提交更改的内容
git commit -m "修改部分代码"  //只有在执行完add后才可以提交更改，参数-m 后可以跟上此次提交的备注
```
> 到这里本地的更改已经可以由本地仓库来进行管理了，如果你需要在多个地点维护你的代码，这时候你就需要将你的代码提交到远程仓库，这里可以提交到GitHub上。
```
//提交本地仓库到GitHub
git push
```
> 当然，我们可以在任何时候查看我们的提交历史记录，或者是查看当前仓库的状态
```
//查看提交历史纪录
git log
//查看当前仓库状态
git status
```
> 这里我给大家一个全套执行的示例  
![检验SSH Key](/Code/Img/Git/Use_Git.gif)  

## GitHub快捷键 ##
> 在GitHub上很多页面都有快捷键，各个页面查看快捷键的方式是按下**shift+/**。

## GitHub使用流程 ##
#### 1.一般流程 ####
* 在GitHub上进行Fork
* 将fork的仓库克隆至本地
* 在本地环境中创建分支
* 修改分支代码并提交至本地
* push代码到fork的仓库中
* 在GitHub上对Fork来源的仓库发送Pull Request  

#### 2.不Fork的开发流程 ####
* 共用一个远程仓库
* 使用不同账户clone项目到本地
* 创建分支修改本地代码并提交
* push到远程仓库
* 在GitHub上合并分支

#### 3.GitHub flow流程 ####
* 令 master 分支时常保持可以部署的状态
* 进行新的作业时要从 master 分支创建新分支，新分支名称要具有描述性
* 在新建的本地仓库分支中进行提交
* 在 GitHub 端仓库创建同名分支，定期 push
* 需要帮助或反馈时创建 Pull Request，以 Pull Request 进行交流
* 让其他开发者进行审查，确认作业完成后与 master 分支合并
* 与 master 分支合并后立刻部署

#### 4.Git flow流程 ####
* 从开发版的分支（develop）创建工作分支（feature branches），进行功能的实现或修正
* 工作分支（feature branches）的修改结束后，与开发版的分支（develop）进行合并
* 重复上述流程，不断实现功能直至可以发布
* 创建用于发布的分支（release branches），处理发布的各项工作
* 发布工作完成后与 master 分支合并，打上版本标签（Tag）进行发布
* 如果发布的软件出现 BUG，以打了标签的版本为基础进行修正（hotfixes）

## Gist ##
> Gist A 是一款简单的 Web 应用程序，常被开发者们用来共享示例代
码和错误信息。其功能有些像简单的，可共享的备忘录，共享时只需将需要共享内容的URL发送给要共享的人即可，共享者之间还可以互相评论留言。当然，他本身也是在Git版本控制的管理之下，可以随时可以查看修改的历史记录，他还支持多种代码高亮。感兴趣的朋友可以试试，这里不再赘述。

## GitHub的GUI客户端##
* [SourceTree](https://www.sourcetreeapp.com/)

## 其他提供类似GitHub功能的开源软件 ##
* [GitBucket](https://github.com/gitbucket/gitbucket)
* [GitLab](http://gitlabhq.com/)
* [Gitorious](https://gitorious.org/)
* [RhodeCode](https://rhodecode.com/)

## 更多 ##
> 本文仅仅展示了最简单的GitHub和git的使用方法，此后会不定期在此文章上更新一些**GitHub**功能的使用方法，至于Git会另写一篇文章专门说明**Git**这个命令的各种参数用法。这里为大家推荐两本书，一本讲述了GitHub的详细使用，书名**《GitHub入门与实践》**，作者是**[日]大塚弘记**。另一本是高级Git的使用方法，书名**《Pro Git》**，不过目前这本书没有中文版，大家也可以参考**《Git版本控制管理（第2版）》**。另外《Pro Git》的英文版是可以从Git的[官网下载](https://git-scm.com/book/en/v2)PDF的。
