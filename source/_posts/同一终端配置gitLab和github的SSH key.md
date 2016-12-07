---
title: 同一终端配置gitLab和github的SSH key
date: 2016-11-08 14:14:33
tags: [ssh key,gitLab,github,git]
---
### 说明
大家都知道配置SSH key后，用git的pull和push时不用输入账户密码了。对于用同一台电脑办公的人来说可能既需要用gitLab又需要用github改如何配置呢？通过以下步骤可以实现gitLab和gitHub项目pull和push的时候都不需要输入密码。
### 步骤
- 在终端，输入命令ls -al ~/.ssh 检查是否显示有id_rsa.pub或者id_dsa.pub存在。
- 键入ssh-keygen -t rsa -C "your_email@example.com"（你的帐号邮箱）
- 一路回车，生成密钥文件(第二次生成时记得更改文件名，例如id_rsa_github)
- 用cat ~/.ssh/id_rsa.pub命令查看文件内容，然后复制出来
- 粘贴到gitLab或者github上的配置中。
- 重复5-7配置另一个帐号
- 打开~/.ssh/config配置文件，输入以下内容：
~~~
#Default account
Host 10.104.100.6/ #主机地址
Hostname gitlab.com #主机名
User xxx@163.com #帐号邮箱
IdentityFile ~/.ssh/id_rsa #ssh key文件地址
#New account
Host github.com
Hostname github.com
User xxx@qq.com
IdentityFile ~/.ssh/id_rsa_github
~~~

