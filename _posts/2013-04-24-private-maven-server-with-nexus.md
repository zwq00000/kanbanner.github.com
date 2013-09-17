---
layout: post
title: "nexus搞起maven私服"
---

从[MAVEN官方](http://maven.apache.org/)下载maven当前最新版本: apache-maven-3.0.5-bin.zip

	解压缩到C:\apache-maven-3.0.5
	新建环境变量并加入到%PATH%: MAVEN_HOME=C:\apache-maven-3.0.5
	命令行执行mvn -v验证maven是否已经正确安装
从[NEXUS官方](http://www.sonatype.org/nexus/go)下载nexus当前最新bundle: nexus-2.3.1-01-bundle.zip

	解压缩到C:\nexus-2.3.1-01-bundle, 如以下目录结构: 
		C:\nexus-2.3.1-01-bundle
			nexus-2.3.1-01
			sonatype-work
	新建环境变量并加入到%PATH%: NEXUS_HOME=C:\nexus-2.3.1-01-bundle\nexus-2.3.1-01
配置NEXUS
	
	JAVA: 
	如果当前没有设置JAVA_HOME环境变量, 则需指定java所在目录, 否则报错
	%NEXUS_HOME%\bin\jsw\conf\wrapper.conf: wrapper.java.command=java

	端口: 
	%NEXUS_HOME%\conf\nexus.properties, application-port, 默认为8081

	修改工作目录: 
	%NEXUS_HOME%\nexus\WEB-INF\plexus.properties
	属性 plexus.nexus-work 或环境变量 PLEXUS_NEXUS_WORK 可定制NEXUS工作目录
	默认为${user.home}/sonatype-work/nexus即%NEXUS_HOME%/../sonatype-work/nexus

安装启动NEXUS

	nexus.bat install<安装service>/uninstall<卸载service>
	nexus.bat start<启动>/stop<停止>

	浏览器http://localhost:8081/nexus访问, 使用admin帐号登录配置。		
NEXUS操作

	NEXUS预置3个用户: 
	  admin: 配置nexus服务权限, 默认密码admin123
	  deployment: 上传部署构件但无法配置nexus权限, 默认密码deployment123
	  anonymous: 未登录用户浏览和搜索仓库权限
	开启远程索引: 
	  download remote index = true
	手工加入第三方jar包: 
	  View/Repositories->Repositories->3rdParty->AntifactUpload->GAVParameters

使NEXUS成为私服

	在settings.xml中配置, 使对本机的所有maven项目有效。
{% highlight xml %}
<profiles>
	<profile>
    	<id>nexus</id>
		<repositories>
      		<repository>
        		<id>nexus</id>
        		<name>nexus repos</name>
        		<url>http://nexus</url><!-- mirrorOf * url已失去意义 -->
        		<releases><enabled>true</enabled></releases>
        		<snapshots><enabled>true</enabled></snapshots>
			</repository>
		</repositories>
		<pluginRepositories>
        	<pluginRepository>
				<id>nexus</id>
				<name>nexus plugin repos</name>
				<url>http://nexus</url><!-- mirrorOf * url已失去意义 -->
				<releases><enabled>true</enabled></releases>
				<snapshots><enabled>true</enabled></snapshots>
			</pluginRepository>
		</pluginRepositories>
	</profile>
</profiles>
<!-- 使profile:nexus有效  -->
<activeProfiles>
	<activeProfile>nexus</activeProfile>
</activeProfiles>
<!-- 使mirror:nexus镜像所有已生效profile  -->
<mirrors>
	<mirror>
    	<id>nexus</id>
        <mirrorOf>*</mirrorOf>
        <url>http://IP:8081/nexus/content/groups/public/</url>
	</mirror>
</mirrors>
{% endhighlight %}

NEXUS是否WORK验证

	执行以下命令, 查看downloading和downloaded项是否是http://IP:8081/nexus/*地址。

	生成maven java项目: 
	mvn archetype:create -DgroupId=com.test -DartifactId=test-app

	生成maven web项目: 
	mvn archetype:create -DgroupId=com.test -DartifactId=test-webapp 
		-DarchetypeArtifactId=maven-archetype-webapp

以上。