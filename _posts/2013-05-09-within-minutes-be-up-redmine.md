---
layout: post
title: "分分钟走你Redmine"
---

基于以下软件和版本：

	bitnami-redmine-2.3.0-2-windows-installer.exe
	bitnami-redmine-2.3.0-2-linux-installer.run

[Bitnami Redmine WIKI](http://wiki.bitnami.com/Applications/BitNami_Redmine), 资料很新, 但没有逐一试验。这里仅记录分享遇到的问题。

版本1.x VS 2.x由来：参考[Redmine News](http://www.redmine.org/news/66)

	Rail core team不再维护Rails2.3, 故Redmine：
		从2.0.0开始升级到Rails3
		1.x分支停留在Rails2.3
	因此导致的插件兼容性问题等, 若缺插件不可, Redmine建议留守1.x

Bitnami Redmine All-in-one installer安装
	
	设置管理员信息和密码, 其它自不必说 

配置邮件SMTP

	C:\BitNami\redmine-2.3.0-2\apps\redmine\htdocs\config\configuration.yml

	default:
	   email_delivery:
	   delivery_method: :smtp
	      smtp_settings:
	         tls: false
			 address: <smtp地址:smtp.email.com>
			 port: 25 <smtp端口>
			 domain: <domain:email.com>
			 authentication: :login
			 user_name: "account@email.com"
			 password: "account_password"
	
测试邮件SMTP

	使用管理员登录, 管理->配置->邮件通知->发送测试邮件

配置使用HTTPS SVN

	Windows成功例：
	cd C:\BitNami\redmine-2.3.0-2\subversion\bin\
	svn ls --config-option config:auth:store-auth-creds=yes 
			--config-dir ssldir https://IP/svn/test
	修改subversion_adapter.rb中credentials_string方法第四行为：
	str << " --no-auth-cache --non-interactive
		 --config-dir C:\\BitNami\\redmine-2.3.0-2\\subversion\\bin\\ssldir"
	重启Redmine
	
	Linux成功例：
	cd /opt/redmine-2.3.0-2/subversion/bin
	svn ls --config-option config:auth:store-auth-creds=yes 
			--config-dir ssldir https://IP/svn/test
	<使apache所在用户和组成为ssldir目录owner>
	ps -ef | grep apache
	ls -al
	sudo chown -R daemon.daemon /opt/redmine-2.3.0-2/subversion/bin/ssldir/
	修改subversion_adapter.rb中credentials_string方法第四行为：
	str << " --no-auth-cache --non-interactive 
		--config-dir /opt/redmine-2.3.0-2/subversion/bin/ssldir"
	重启Redmine

测试SVN是否连通

	项目->版本库, 正常拉取版本库内容

配置使用GIT

	Redmine目前仅支持通过文件系统存取本机Git REPOS。
	PATH=/opt/redmine-2.3.0-2/git/bin:$PATH<添加git到PATH>
	echo $PATH | grep git
	
	cd /opt/redmine-2.3.0-2/git/bin
	git clone URL_REDMINE_GIT<拉取Git REPOS到本机路径>
	Redmine->项目->配置->版本库中选择配置GIT。
	库路径：/opt/redmine-2.3.0-2/git/bin/URL_REDMINE_GIT/.git

	新增linux计划任务(cron task)使Redmine自动获取Git REPOS最近更新。
	cd /opt/redmine-2.3.0-2/git/bin
	vi redmine_git_changesets.sh
	cd /opt/redmine-2.3.0-2/git/bin/URL_REDMINE_GIT && git pull origin master
	:wq<保存退出>
	chmod 744 /opt/redmine-2.3.0-2/git/bin/redmine_git_changesets.sh
	测试手动执行/opt/redmine-2.3.0-2/git/bin/redmine_git_changesets.sh, OK!

	crontab -e
	* * * * * /opt/redmine-2.3.0-2/git/bin/redmine_git_changesets.sh

以上。
<br>