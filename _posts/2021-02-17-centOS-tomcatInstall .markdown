---

layout: post
title: '[centOS]Linux에 tomcat설치 및 설정'
subtitle: '[centOS]Linux에 tomcat설치 및 설정'
categories: devlog
tags: centOS
comments: true

---


# tomcat 설치 및 설정

0. 작업은 /root

1. tomcat8 다운로드
   ```wget https://mirror.navercorp.com/apache/tomcat/tomcat-8/v8.5.65/bin/apache-tomcat-8.5.65.tar.gz```

   안되면 https://mirror.navercorp.com 들어가서 위 링크대로 tomcat까지들어가서 새로운 버전 tar.gz 윈도우에 받고 sftp로 ssh서버에 put하기

2. 압축 풀기  
   ``` tar xvfz apache-tomcat-8.5.65.tar.gz```

3. 설치  
   ``` mv apache-tomcat-8.5.65 /usr/local/douzone/tomcat8.5```  
   ``` ln -s /usr/local/douzone/tomcat8.5 /usr/local/douzone/tomcat```  

4. 설정(/etc/profile, 생략)  


5. 포트 확인 및 변경  
   ```vi /usr/local/douzone/tomcat/conf/server.xml```


	강의에서 약속  
	서버에서 실행 포트 : 8088 ,로컬에서 실행 포트 : 8080  
	명령어 모드에서 단어(ex:8080) 검색하는방법  
	/8080  
	vi /usr/local/douzone/tomcat/conf/server.xml  

	-----------Insert모드----------------
	```
	Connector port = "8088"로 변경
	```


6. 실행  
	tomcat 실행전 상태
	![image](https://user-images.githubusercontent.com/60701130/154419149-964ddb15-dbdb-4db4-9ccb-6037db4b72e6.png)
	
	tomcat 실행
	```/usr/local/douzone/tomcat/bin/catalina.sh start```  
	![image](https://user-images.githubusercontent.com/60701130/154419542-806e55c2-fd38-4160-bd5d-44c1fb4390b2.png)

	``` ps -ef | grep tomcat```  
	![image](https://user-images.githubusercontent.com/60701130/154419412-72333ba6-e34f-47c4-84ff-e436a5d9e418.png)

	``` ps -ef | grep java```  
	![image](https://user-images.githubusercontent.com/60701130/154419452-e2965ff6-8037-47ec-8ed6-be5312d445a1.png)


7. 브라우저로 접근 하기  
   http://자기IPADDR:8088  
   ![image](https://user-images.githubusercontent.com/60701130/154419819-5c36effa-cdae-4a0a-9077-beda0e15c50f.png)


8. 중지 시키기  
   ```/usr/local/douzone/tomcat/bin/catalina.sh stop```

9. 서비스 등록 하기  
   파일 생성  
   ```vi /usr/lib/systemd/system/tomcat.service ```  

	```
	[UNIT]
	Description=tomcat8
	After=syslog.target network.target

	[Service]
	Type=forking

	Environment="JAVA_HOME=/usr/local/douzone/java"
	Environment="CATALINA_HOME=/usr/local/douzone/tomcat"

	ExecStart=/usr/local/douzone/tomcat/bin/startup.sh
	ExecStop=/usr/local/douzone/tomcat/bin/shutdown.sh

	User=root
	Group=root

	[Install]
	WantedBy=multi-user.target
	```

   등록  
   ```systemctl enable tomcat```  

10. tomcat 서비스 실행/중지/재실행  
   ```systemctl start tomcat```  
   ``` systemctl stop tomcat```   
   ``` systemctl restart tomcat```  

11. tomcat manager 설정  
   1) tomcat-users.xml 설정  
       ```vi /usr/local/douzone/tomcat/conf/tomcat-users.xml```  
	
		1-1) /tomcat-users 바로위에 붙여넣어야할 내용  	
		```
		<role rolename="manager"/>
		<role rolename="manager-gui" />
		<role rolename="manager-script" />
		<role rolename="manager-jmx" />
		<role rolename="manager-status" />
		<role rolename="admin"/>
		<user username="admin" password="manager" roles="admin,manager,manager-gui, manager-script, manager-jmx, manager-status"/>
		```
	

   2) contect.xml 설정  
   ```vi /usr/local/douzone/tomcat/webapps/manager/META-INF/context.xml```

- 이전 내용
	![image](https://user-images.githubusercontent.com/60701130/154430796-93be374d-9ea4-4e79-be19-5e37aab33ff4.png)

- 설정 변경 후
![image](https://user-images.githubusercontent.com/60701130/154430940-1b1fd238-7ba9-4e61-8bc5-317f9651e611.png)

- 추가 및 변경된 내용
	```
	<Context antiResourceLocking="false" privileged="true" docBase="${catalina.home}/webapps/manager">
	<Valve className="org.apache.catalina.valves.RemoteAddrValve"
			allow="^.*$" />
	</Context>
	```

12. tomcat 재시작
    ``` systemctl stop tomcat```    
    ``` ps -ef | grep tomcat```    
    ``` systemctl start tomcat```  

13. 확인하기  
	http://자기IPAddr/manager 

-	비밀번호는  tomcat-users.xml 설정 시 맨밑구문   
	```
	<user username="admin" password="manager" roles="admin,manager,manager-gui, manager-script, manager-jmx, manager-status"/>
	```

![image](https://user-images.githubusercontent.com/60701130/154431399-0d878a52-ed55-43dd-a52d-e0190c583e2b.png)
  






 
 

    