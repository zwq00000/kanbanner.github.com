---
layout: post
title: "分分钟走你SVN"
---

搭建内部SVN版本管理平台可有以下三种选择: 

	Apache + Subversion
	VisualSVN Server
	CollabNet Subversion Edge

优缺点比较: 

	Apache + Subversion
		手工配置, 稍复杂但足够灵活; 多平台; 可配置多协议支持http/https/svn
	VisualSVN Server
		足够简单; 仅Windows平台; 支持http/https协议; ldap模块需license
	CollabNet Subversion Edge
		功能强大, 相对简单; 多平台支持; 支持http/https协议;
		FREE and completely open source

本篇基于以下软件和版本: 

	CollabNetSubversionEdge-3.3.2_setup-x86_64.exe

从安装到就绪: 
	
	安装(jre支持)->等待CollabNetSubversionEdge控制台准备OK
	->通过http://IP:3343/CSVN/访问->登陆(初始账号admin/admin)->启动Subversion服务器
	
下面记录几个实践: 

HTTPS方式访问

	管理->Server Settings->勾选Apache加密 Subversion服务器应通过https提供服务->保存

SVN版本库创建|模板|备份

	管理->Server Settings 可设置版本库和备份路径
		版本库父文件夹 默认%CSVN%\data\repositories
		Backup Directory 默认%CSVN%\data\dumps
		
	版本库->创建
		从SVN版本库模板创建
		从SVN备份文件创建
	
	版本库->Manage Templates
		系统自带2个模板, 可自定义模板:
			Empty repository
			标准trunk/branches/tag结构
		
	版本库->Backup Schedule
		常用两种备份方式: 
			Full Dump Backup
			Hotcopy Backup
		
SVN版本库访问权限控制, 例: 
	[groups]
		devs = jim, joe, bill, john, mary 
		mgrs = john, mary
		docs = sue, john
		
	[/]
		* = r
		@mgrs = rw
		
	[test:/]
		@devs = rw
		
	[test:/tags]
		@devs = r
		
	[test:/trunk/docs]
		@docs = rw
访问方式
	
	控制台: https://IP/viewvc/test/
	客户端/浏览器: https://IP/svn/test/
	

参考资料链接: 
>
[Quick overview Slideshow](http://www.collab.net/products/subversion/capabilities)<br>
[笔记1: 基本安装设定](http://blog.miniasp.com/post/2011/12/30/CollabNet-Subversion-Edge-Installation-Notes-Part-1-Basic.aspx)<br>
[笔记2: 整合AD域](http://blog.miniasp.com/post/2012/01/03/CollabNet-Subversion-Edge-Installation-Notes-Part-2-Active-Directory-Integration.aspx)<br>
[笔记3: 安装SSL凭证](http://blog.miniasp.com/post/2012/01/14/CollabNet-Subversion-Edge-Installation-Notes-Part-3-HTTPS-SSL-Certificate.aspx)<br>
[笔记4: 自定义版本库模板](http://blog.miniasp.com/post/2012/03/29/CollabNet-Subversion-Edge-Installation-Notes-Part-4-Repository-Template.aspx)
>

以上。