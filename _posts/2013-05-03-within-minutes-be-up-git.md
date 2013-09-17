---
layout: post
title: "分分钟走你Git"
---

搭建内部Git版本管理平台有两种选择：

	Windows Gitblit
	Linux Gitlab

Windows2008 Server R2环境, Gitblit搭建Git Server实践记录。

Gitblit官方网站: [戳这里](http://gitblit.com/), 最新2013-01-15版本1.2.1, GO版本, 需Java运行环境支持。

	解压缩到C:/gitblit-1.2.1, 修改C:/gitblit-1.2.1/data/gitblit.properties
	修改配置项server.contextPath = /gitblit, 保存启动gitblit.cmd
		建立8443端口的https连接, 可通过https://localhost:8443/gitblit访问	
	修改配置项: server.httpPort = 8080, server.httpsPort = 0, 保存启动gitblit.cmd
		建立8080端口的http连接, 可通过http://localhost:8080/gitblit访问

	默认git库目录配置项git.repositoriesFolder = ${baseFolder}/git
	即C:/gitblit-1.2.1/data/git, 修改到d:/gitblitREPOs

	通过installService.cmd/uninstallService.cmd, 可安装/卸载windows gitblit服务

	创建git库: gitblit-test, 尝试进行clone, push, pull等操作

	以上即可把gitblit搭建的Git Server使用起来, 更多可参考官方网站

	优点: GO/WAR等多版本可用;通过Manager可远程管理Gitblit server;federation备份策略等
	缺点: 版本更新慢;尚不支持PR等;用户较少等

Gitlab, Ubuntu 10.04 LTS环境, 实践记录。

官方网站: [戳这里](http://gitlab.org/), 最新版本5.1.0-3, 下载使用BitNami Gitlab Stack: [戳这里](http://bitnami.com/stack/gitlab)。

查看REPO Tree

备份

CodeReview

Fork/PR/MR

Issue2PR


