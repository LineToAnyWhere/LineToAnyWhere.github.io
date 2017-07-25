# Mail #
> # Mail简介 #

要发送一封邮件，通常需要MUA（Mail User Agent）、MTA(Mail Transfer Agent)、MDA(Mail Delivery Agent)三个主要组件，下面简单介绍一下在发送邮件的整个过程中处理的流程：
* **取得MTA的权限（即获取email帐号密码）**
* **在MUA上编写邮件（收发地址以及邮件内容），传送到MTA**
* **如果该邮件的目标是本地端MTA自己的帐号，则邮件被送到相应的Mailbox**
* **如果该邮件的目的为其他的MTA，则还是转递(Relay)流程**
* **对方MTA服务器收到邮件**  

要接受邮件，通常需要MRA(Mail Retrieval Agent)组件，使用者通过MRA提供的POP协议接收邮件，也可以通过IMAP协议将自己的邮件保留在邮件主机上。
> # Mail安装 #

> # Mail配置 #

> # Mail使用 #
