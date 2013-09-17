---
layout: post
title: "安装WAS和补丁"
---

安装WASND7和补丁, Windows2008R2环境, 实践无错记录。

基于以下软件和版本: 

	C1G2JML.zip
	7.0.0.27-WS-UPDI-WinAMD64.zip
	7.0.0-WS-WAS-WinX64-FP0000027.pak
	7.0.0-WS-WASSDK-WinX64-FP0000027.pak
安装前确认: 1.中文安装向导; 2.避免乱码

	控制面板->区域和语言->管理->非Unicode程序的语言: 中文(简体, 中国), 需重启
1.  安装WAS7(仅注意以下位置, 其他默认即可)

		启动C1G2JML\launchpad.exe进行安装
		安装可选的功能部件: 
			安装管理控制台的非英语语言软件包
			安装应用程序服务器运行时环境的非英语语言软件包
		安装目录: C:\IBM\WebSphere\AppServer
		Websphere Application Server环境: 无 
			安装好WAS7和补丁后, 由概要管理工具统一创建
2.  安装UpdateInstaller(注意以下位置, 其他默认即可)

		启动7.0.0.27-WS-UPDI-WinAMD64\UpdateInstaller\install.exe进行安装
		安装目录: C:\IBM\WebSphere\UpdateInstaller
3.  安装升级补丁(注意以下位置, 其他默认即可)

		输入要更新的产品的安装位置: C:\IBM\WebSphere\AppServer
		安装维护软件包, 拷贝到C:\IBM\WebSphere\UpdateInstaller\maintenance目录: 
			7.0.0-WS-WAS-WinX64-FP0000027.pak
			7.0.0-WS-WASSDK-WinX64-FP0000027.pak
4.  概要管理工具(Profile Management Tool)
		
		WASND7版本支持五种特定类型的环境：
			单元(Deployment Manager和联合应用程序服务器)
			管理
			应用程序服务器
			定制概要文件
			安全代理(仅用于配置)
5.	创建应用程序服务器AppSrv01

		概要管理工具->应用程序服务器->典型概要文件->启用管理安全性->...
6.	安装验证|启动服务器|管理控制台

		使用【启用管理安全性】处设置的账号和密码, 登陆集成方案控制台
			https://ip:9043/ibm/console/logon.jsp
				
		验证Websphere Application Server套件版本: 7.0.0.27

以上。
<br>
