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

2013/09/20补充: 
		现象: 
			Pages在本地调试预览正常显示, 提交到github后页面没有更新
		RootCause:
			page build failed(邮件和github repository设置页中均有此提示)
		解决：
			本地和github pages ci服务器jekyll版本不一致, 导致代码和配置不能编译通过
			github帮助页面Syntax errors节可以看到ci服务器jekyll版本
			https://help.github.com/articles/pages-don-t-build-unable-to-run-jekyll
			执行gem list命令可以看到本地使用jekyll版本。

			执行gem update更新jekyll版本
			gem uninstall pygments.rb卸载掉所有pygments.rb
			gem install pygments.rb --version="0.5.0"重新安装pygments.rb

			_config.yml配置文件中删除auto: true项, 增加excerpt_separator: ""项

			本地执行jekyll server watch命令编译预览, PASS！！
			COMMIT PUSH到github, 可即时更新, PASS！！

以上。
<br>
