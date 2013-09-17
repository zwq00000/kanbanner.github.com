---
layout: post
title: "用Jekyll写Github Pages"
---

用Jekyll写Github Pages, Windows7环境, 实践无错记录。

基于以下软件和版本: 

	msysGit-fullinstall-1.8.1.2-preview20130201.exe
	rubyinstaller-1.9.3-p392.exe
	python-2.7.3.msi
	DevKit-tdm-32-4.5.2-20111229-1559-sfx.exe
	git-credential-winstore.exe

步骤: <br>

1. 注册[Github](https://github.com/signup/free)帐号(user), 创建新REPO, 全名(user.github.com)<br>
2. 下载并安装[msysgit](https://code.google.com/p/msysgit/downloads/list), 安装位置: C:\msysgit<br>
3. msys.bat生成SSH Key

		$ cd ~/.ssh<是否存在.ssh目录>
		$ ls
		    config  id_rsa  id_rsa.pub  known_hosts
		$ mkdir key_backup
		$ cp id_rsa* key_backup<如存在, 则备份>
		$ rm id_rsa*
		$ ssh-keygen -t rsa -C "user#email.com"
		    Generating public/private rsa key pair.
		    Enter file in which to save the key (~/.ssh/id_rsa):<回车>
		    Enter passphrase (empty for no passphrase):<输入密钥>
		    Enter same passphrase again:<输入密钥>
4. 将id_rsa.pub内容添加到Github->Account Settings->SSH Keys项
5. 测试连接情况

		$ ssh -T git@github.com
		    The authenticity of host 'github.com (207.97.227.239)' can't be established.
		    RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
		    Are you sure you want to continue connecting (yes/no)?<yes>

		    Hi user! 
		    You've successfully authenticated, but GitHub does not provide shell access.
6.  设置全局信息

		$ git config --global user.name "user"
		$ git config --global user.email "user#email.com"
7.  Clone并提交REPO

		$ git clone https://github.com/user/user.github.com.git
		$ git clone https://github.com/plusjade/jekyll-bootstrap.git

		拷贝jekyll-bootstrap下面所有内容(隐藏.git目录除外)到user.github.com中

		提交到github: 
		$ git add .
		$ git commit -m "Creating_initial_branch_structure"
		$ git push origin master<输入rsa密钥>
8.  几分钟后浏览http://user.github.com, It Works!<br>


以上。
<br>
