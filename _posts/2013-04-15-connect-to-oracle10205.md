---
layout: post
title: "连接到Oracle10.2.0.5"
---

连接到数据库Oracle10.2.0.5, 远程/本地, 客户端: sqldbx和plsql developer, 实践无错记录。

基于以下软件和版本: 

	instantclient-basic-win32-10.2.0.5.zip
	sqldbx
	plsql developer
PS: <br>
客户端(sqldbx和plsql developer等)需借助32位instantclient连接到64位Oracle<br>
sqldbx个人版本, 免费但不支持Unicode; 专业版本, 收费支持Unicode<br>

1.  本地连接(sqldbx和plsql developer)

		解压缩instantclient到C:\oracle\instantclient_10_2
		创建目录并复制C:\oracle\instantclient_10_2\network\ADMIN\tnsnames.ora

		sqldbx中: 
		Tools->Options->Servers中设置Additional Oracle Home：
			client,C:\oracle\instantclient_10_2

		plsql developer中: 
		Tools->Preferences->Oracle Connection中设置：
			Oralce Home：C:\oracle\instantclient_10_2
			OCI library：C:\oracle\instantclient_10_2\oci.dll

		测试可以正常连接
2.  免安装ORACLE客户端远程连接(sqldbx和plsql developer)

		解压缩instantclient到C:\instantclient_10_2
		设置环境变量ORACLE_HOME = C:\instantclient_10_2

		创建目录并复制C:\instantclient_10_2\network\ADMIN\tnsnames.ora
		修改tnsnames.ora中HOST/PORT为正确的oracle服务器IP地址和端口

		设置环境变量: NLS_LANG = AMERICAN_AMERICA.AL32UTF8

		sqldbx中: 
		Tools->Options->Servers中设置Additional Oracle Home: 
			client,C:\instantclient_10_2

		plsql developer中: 
		Tools->Preferences->Oracle Connection中设置: 
			Oralce Home: C:\instantclient_10_2
			OCI library: C:\instantclient_10_2\oci.dll

		测试可以正常连接

以上。
<br>