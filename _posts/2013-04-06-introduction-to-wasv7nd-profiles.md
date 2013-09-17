---
layout: post
title: "Introduction to WASv7ND Profiles"
---

WASv7ND版本可以创建五种特定类型环境:  
	
	单元(Deployment Manager和联合应用程序服务器)
	管理
	应用程序服务器
	定制概要文件
	安全代理(仅用于配置)
单元(Deployment Manager和联合应用程序服务器)

	一个单元环境创建两个概要文件: 即一个包含Deployment Manager的管理概要文件和一个应用
	程序服务器概要文件。应用程序服务器与Deployment Manager的单元联合。
管理
	
	管理概要文件提供了用于管理多个应用程序服务器环境的服务器和服务。
	管理代理程序可管理同一机器上的应用程序服务器。
	此Network Deployment版本还包含用于紧耦合管理的Deployment Manager以及用于对分布在多台
	机器上的拓扑进行松耦合管理的作业管理器。
应用程序服务器
	
	应用程序服务器环境运行企业应用程序。
	对WebSphere Application Server的管理是从它自己的管理控制台进行的, 它的工作与所有其他
	应用程序服务器无关。
定制概要文件
	
	定制概要文件包含一个空节点, 该节点未包含管理控制台或服务器。
	定制概要文件的典型用法是将它的节点联合到Deployment Manager。
	联合节点后, 使用Deployment Manager在该节点内创建服务器或服务器集群。
安全代理(仅用于配置)
	
	安全代理仅用于配置的概要文件供DMZ安全代理服务器使用。
	您不能在Network Deployment按章中启动安全代理服务器。
	此仅用于配置的概要文件仅用于通过管理控制台来配置概要文件。
	在配置概要文件之后, 可以到处概要配置文件, 然后将该配置导入DMZ中的安全代理概要文件。

更多详细介绍可参考 WASv7红宝书: <br>
WebSphere Application Server V7 Administration and Configuration Guide

<br>
使用PMT GUI方式创建某特定类型环境时, 一般有典型和高级概要文件两种选择: <br>

高级概要文件
	
	可定制是否启用管理安全性; 端口值分配; 作为Windows服务运行; 创建WEB服务器定义等。
典型概要文件

	可定制是否启用管理安全性; 其他默认值。

可参考IBM developerworks的WASv7系统管理系列文章: <br>
[第1部分: 管理增强功能概述](http://www.ibm.com/developerworks/cn/websphere/techjournal/0811_apte/0811_apte.html)<br>
[第2部分: 新的管理拓扑](http://www.ibm.com/developerworks/cn/websphere/techjournal/0901_cundiff/0901_cundiff.html)<br>
[第3部分: 管理灵活的管理拓扑](http://www.ibm.com/developerworks/cn/websphere/techjournal/0903_khalil/)<br>
[第4部分: 基于属性的配置](http://www.ibm.com/developerworks/cn/websphere/techjournal/0904_chang/0904_chang.html)<br>
[第5部分: 业务级应用程序](http://www.ibm.com/developerworks/cn/websphere/techjournal/0905_edwards/0905_edwards.html)

以上。
<br>