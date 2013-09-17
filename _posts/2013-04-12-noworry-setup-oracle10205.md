---
layout: post
title: "无错安装Oracle10.2.0.5"
---

安装Oracle10.2.0.5, Windows2008R2环境, 实践无错记录。

基于以下软件和版本: 

	10204_vista_w2k8_x64_production_db.zip
	p8202632_10205_MSWIN-x86-64.zip
	p8350262_10205_Generic.zip
1.  安装Oracle10204, 不创建启动数据库

		修改下面两处, 通过先决条件检查: 
			第一处：%DATABASE%\stage\prereq\db\refhost.xml
				增加以下内容到恰当位置
					<OPERATING_SYSTEM>
			    		<VERSION VALUE="6.1"/>
					</OPERATING_SYSTEM>

			第二处：%DATABASE%\install\oraparam.ini
			    [Certified Versions]
			    	Windows=5.0,5.1,5.2,6.0,6.1<此处增加值项6.1>
			    增加以下内容到恰当位置
			    	[Windows-6.1-optional]

		安装主目录: 
			OraDb10g_home1 = C:\oracle\product\10.2.0\db_1
2.  升级安装Oracle10205

		参考上面步骤, 通过先决条件检查
		参考上面步骤, 指定主目录详细信息为OraDb10g_home1
3.  apply补丁p8350262_10205_Generic

		设置两个环境变量: 
			ORACLE_HOME = C:\oracle\product\10.2.0\db_1
			ORACLE_SID = ORCL<随便取个名字先>

		命令行切换到%p8350262_10205_Generic%\8350262\执行以下命令安装EM证书过期补丁: 
			%ORACLE_HOME%\OPatch\opatch apply

		为避免不必要的麻烦, 成功安装证书补丁后, 删除环境变量ORACLE_SID
4.  Net Configuration Assistant创建LISTENER

		监听程序配置->添加 ... <使用默认值>
5.  DBCA创建数据库<ORCL>

		初始化参数: 使用Unicode(AL32UTF8)字符集存储多语言组

		--设置环境变量NLS_LANG为以下查询结果值
		SELECT USERENV('LANGUAGE') FROM DUAL;
6.  sqlplus确认数据库版本

		命令行敲入sqlplus, 输入帐号和密码, 确认数据库环境和版本：
		Connected to: 
			Oracle Database 10g Enterprise Edition Release 10.2.0.5.0 - 64bit Production
			With the Partitioning, OLAP, Data Mining and Real Application Testing options
		
		--查看当前登录ORACLE_SID
		SELECT NAME FROM V$DATABASE;
		--查看当前登录帐号
		SELECT SYS.LOGIN_USER FROM DUAL;

以上。
<br>