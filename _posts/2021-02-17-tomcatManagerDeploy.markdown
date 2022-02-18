---

layout: post
title: '[tomcatManager]Hello World 배포하기'
subtitle: '[tomcatManager]Hello World 배포하기'
categories: devlog
tags: deploy
comments: true

---

# 환경
centOS7(VMWare)에 tomcat 설치함  


# war파일, 톰캣 매니저 활용해서 어플리케이션 배포하기

## maven project 생성
- file -new - project - maven - maven prject - create a simple project(체크) - next    
group id : com.douzone  (보통 회사이름)  
artifact id : javastudy    
packaging은 pom 체크 (부모가 폼이 돼야하기 때문)  

	부모는 src 폴더 없어도 됨 (삭제하기)  


## maven module 생성(war 파일)
- new - project - maven - maven module - reate a simple project(체크) - next  
ex) group id : com.douzone    
artifact id : javastudy    
packaging은 war 체크  

- web.xml생성하기  
프로젝트 우클릭 - JAVA EE Tools - Generate Deployment Descriptor Stub  

## 톰캣 설정하기  
- window - preferences- server- runtime Environment - add - 8.5 버전선택  
Tomcat installation directory에 C:\douzone\apache-tomcat-8.5.75 넣기  
	- 톰캣홈페이지 zip 파일 맨위에거 다운(더존파일에압축풀기)  
		또는  https://mirror.navercorp.com 들어가서 tomcat까지들어가서 새로운 버전 zip 파일 받기  

	피니시 - apply close  


- 프로젝트 우클릭 - properties - Project Facets - Java 선택후 우측에 Runtimes - 톰캣8.5체크 - apply - ok

- 콘솔창쪽 server 클릭 , 링크클릭 8.5v 선택후 next - 톰캣에 띄우고싶은 프로젝트 configured로 옮기기 - finish  

### 이클립스에서 war파일만들기  
- file - export - web - warfile - next - web project: war파일로 만들 		프로젝트선택 - Broswe - war파일 저장할 경로선택 - Target runtime에 		tomcatv8.5선택 - Export source files 는 기본적으로는 체크를 해제하며 		고객사에게 소스(.java) 파일까지 제공할 경우 체크  

	`배포할때는 webapp 바로밑에 index.jsp 만들어야함`

### war파일 배포하기

#### 1. 윈도우에서 배포하기

- {tomcat 설치 경로}\webapps 폴더에 생성한 war 파일을 복사한다.  

- {tomcat 설치 경로}\bin 으로 들어가서 startup.bat을 실행하면 tomcat이 시작된다.  
- tomcat을 시작하면, 자동으로 프로젝트 이름과 동일한 폴더가 생성되면서 war 파일로 묶여있던 패키지가 풀린다.  
- tomcat경로/conf에서 server.xml 열어서 밑에 내용 추가하기(ContextPath 설정)  
	```
	<Host ~> 
		<Context path="" docBase="war파일명" reloadable="false" />
	</Host>    
	```
- http://localhost:8080/war파일명 또는 http://IPAddr:8080/war파일명 로 접속하면 만들어 놓은 index.jsp 에 접속됨

#### 2. 리눅스에서 배포하기

- war 파일 복사해서 tomcat이 설치된 디렉토리의 webapps 디렉토리에 붙여넣고
		war파일 이름이 root가 아니라면 tomcat경로/conf 들어가서 server.xml 내용 추가해야함(contextPath 설정)  
		```vi server.xml```  
		
		
		<Host ~> 
			<Context path="" docBase="war파일명" reloadable="false" />
		</Host>  
		


- tomcat을 재실행한다.  
	(1) 서비스 등록했을 때    
	```systemctl restart tomcat```  
	(2) 등록 안돼있을 때  
	tomcat경로/bin/startup.sh 실행  


- Windows와 동일하게 tomcat을 시작하면 자동으로 프로젝트 이름과 동일한 폴더가 생성되면서 war 파일로 묶여있던 패키지가 풀린다.


