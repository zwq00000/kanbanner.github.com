---
layout: post
title: "WAS几个配置项"
---
WAS几个配置项, Windows2008R2+WASv7ND环境, 实践无错记录。

1.WAS时区设置
	管理控制台->服务器/服务器类型/WebSphere Application Server->
	选择应用程序服务器(例: server1)->服务器基础结构->Java和进程管理
	->进程定义->Java虚拟机->定制属性

	新建属性键值对: 名称: user.timezone, 值: Asia/Shanghai or GMT+8
	保存并重启该应用程序服务器(例: server1)
2.WAS日志路径
	例: %IBM\WebSphere%\AppServer\profiles\AppSrv01\logs\server1\
3.WAS应用程序安装路径
	例: %IBM\WebSphere%\AppServer\profiles\AppSrv01\installedApps\%WAS_CELL_NAME%\
4.建立WAS变量
	管理控制台->环境->WebSphere变量->选择变量有效作用域(例: 单元)
	新建变量键值对: 名称:WAS_DIR_JCO, 值: %IBM\WebSphere%\JCO
5.建立和引用WAS共享库(例:JCO_SharedLib)
	新建共享库
		管理控制台->环境->共享库->选择共享库引用作用域(例:单元)

		新建共享库: 名称: JCO_SharedLib, 类路径: %IBM\WebSphere%\JCO\sapjco3.jar
		本机库路径: %IBM\WebSphere%\JCO\libsapjco3.so
				    %IBM\WebSphere%\JCO\sapjco3.dll
		注意: 
		1.使用回车分隔多个类路径
		2.共享库中引用的WAS变量须保证有效作用域相同, 或可使用绝对路径
		3.请对此共享库使用隔离的类装入器
			单例模式, 在多个应用程序引用该共享库时只有一个实例版本
		
		点击应用确定保存并返回

	应用程序(例: test)层面共享
		管理控制台->应用程序->应用程序类型->WebSphere企业应用程序
		->点击test链接进入应用程序test配置页面->引用->共享库引用
		勾选test并点引用共享库按钮, 将需要引用的共享库从可用项侧移动到已选项侧

	应用程序服务器(例: server1)层面共享
		管理控制台->服务器/服务器类型/WebSphere Application Server->
		选择应用程序服务器(例: server1)->服务器基础结构->Java和进程管理->类装入器
		->新建->选择类装入器顺序->应用确定保存

		点击该类装入器链接进入类装入器配置页面->共享库引用->添加->选择共享库名
		->应用确定, 重复操作可添加引用多个共享库

		保存并重启该应用程序服务器(例: server1)

以上, 后面将陆续记录WAS配置项。
<br>