---
layout: post
title: "Github Pages本地预览"
---

本地预览Github Pages, Windows7环境, 实践无错记录。

步骤: <br>

1.	安装ruby & python, 解压缩devkit到c:\devkit<br>
2.	命令行下切换到c:\devkit

		ruby dk.rb init
		ruby dk.rb install
		gem sources -l
		gem sources --remove http://rubygems.org/ 
		gem sources -a http://ruby.taobao.org/<使用taobao源>
		gem install jekyll
		gem install rdiscount -v=1.6.8 --platform=ruby<指定-v和--platform, 否则报错>
3.	涉及显示中文/日文等, 需设置LANG和LC_ALL两个环境变量, 其值均为zh_CN.UTF-8<br>
4.  在user.gitub.com目录中执行: jekyll --server, 通过http://localhost:4000访问预览

		已经安装directory_watcher, 但--auto参数仍然无效, 请懂的xdjm吱声！
5.  Windows7使用[git-credential-winstore](http://gitcredentialstore.codeplex.com/)记住密码

		https方式与github交互
		下载并拷贝git-credential-winstore.exe到c:\msysgit\bin\<与git.exe相同位置>
		第一次提交时会弹出Git Credentials Windows安全对话框, 输入帐号和密码
			<使用登录https://github.com的帐号和密码, 而不是SSH Key>
		以后再提交时, 已无需输入账号和密码
			密码凭据: 控制面板->用户帐号->管理您的凭据->普通凭据(git:https://github.com)
6.	OS X 10.8.3使用~/.netrc记住密码

		vi ~/.netrc<输入以下3行内容>
			machine github.com
			login your_account
			password your_password
		:wq
		以后再提交时, 已无需输入账号和密码。

以上。
<br>
