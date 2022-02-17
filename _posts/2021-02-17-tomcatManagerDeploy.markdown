---

layout: post
title: '[tomcatManager]Hello World 배포하기'
subtitle: '[tomcatManager]Hello World 배포하기'
categories: devlog
tags: deploy
comments: true

---

# war파일, 톰캣 매니저 활용해서 어플리케이션 배포하기

## maven project 생성
file -new - project - maven - maven prject - create a simple project(체크) - next    
group id : com.douzone  (보통 회사이름)  
artifact id : javastudy    
packaging은 pom 체크 (부모가 폼이 돼야하기 때문)  

부모는 src 폴더 없어도 됨 (삭제하기)  


## maven module 생성(war 파일)
new - project - maven - maven module - reate a simple project(체크) - next  
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


프로젝트 우클릭 - properties - Project Facets - Java 선택후 우측에 Runtimes - 톰캣8.5체크 - apply - ok

콘솔창쪽 server 클릭 , 링크클릭 8.5v 선택후 next - 톰캣에 띄우고싶은 프로젝트 configured로 옮기기 - finish  

### 이클립스에서 war파일만들기  
file - export - web - warfile - next - web project: war파일로 만들 프로젝트선택 - Broswe - war파일 저장할 경로선택 - Target runtime에 tomcatv8.5선택 - Export source files 는 기본적으로는 체크를 해제하며 고객사에게 소스(.java) 파일까지 제공할 경우 체크

### 윈도우에서 배포하기

- {tomcat 설치 경로}\webapps 폴더에 생성한 war 파일을 복사한다.  

- {tomcat 설치 경로}/bin 으로 들어가서 startup.bat을 실행하면 tomcat이 시작된다.  
- tomcat을 시작하면, 자동으로 프로젝트 이름과 동일한 폴더가 생성되면서 war 파일로 묶여있던 패키지가 풀린다.  
- 웹브라우저에서 localhost:8080이나 아이피주소:8080로 해당 프로젝트에 접속하면 된다.   
- 프로젝트명이 test인 경우 http://localhost:8080/test 로 접속하면 spring 프로젝트에 접속된다.

### 리눅스에서 배포하기

tomcat이 설치된 디렉토리의 webapps 디렉토리에 war 파일을 복사하고 tomcat을 재시작 해주면 된다.

(/var/lib/tomcat{버전}/webapps/ 디렉토리에 복사한다.)



tomcat을 재실행한다.

Windows와 동일하게 tomcat을 시작하면 자동으로 프로젝트 이름과 동일한 폴더가 생성되면서 war 파일로 묶여있던 패키지가 풀린다.



$ sudo service tomcat{버전} restart



웹브라우저에서 해당 서버의 아이피주소:8080로 접속할 수 있다.




new -web의  dynamic web project- 프로젝트 네임 설정 - next - next - generate web.xml deployment descriptor 체크후 finish
webapp 폴더 우클릭 (index.jsp)jsp 파일 생성
window- preferences- server- runtime -Environment - add - 8.5 버전선택
Tomcat installation directory에 C:\douzone2021\apache-tomcat-8.5.71 넣기
피니시 - apply close
톰캣홈페이지 zip 파일 맨위에거 다운(더존파일에압축풀기)
콘솔창쪽 server 클릭 , 링크클릭 8.5v 선택후 next 
프로젝트 우클릭 프로퍼티 - project facets - dynamic web module 버전 3.1정도로 바꾸기, java는 1.8정도로 바꾸기
오른쪽에 Runtimes - Tomcat v8.5 선택 -  apply
콘솔창쪽 server 클릭 , 링크클릭 8.5v 선택후 next - add하기 - finish
프로젝트 우클릭-  프로퍼티 -  자바 빌드패쓰 들어가서 libraries - 서버런타임확인
콘솔창쪽에 서버 클릭해서 오른쪽위에 실행키 눌려주기
localhost:8080 접속안됨 : 어플리케이션 지정안해서 404에러
localhost:8080/helloweb


이클립스에서 war파일만들기
file - export - web - warfile - next - Broswe - douzone선택 helloweb\helloweb.war
localhost:8088 로그인한 화면에서 war파일 추가
배치 눌리면 배포됨
xshell에서 webapps폴더에서 ls -l하면 helloweb.war파일 들어가있음
cd helloweb 하면 index.jsp 있음
localhost:8088/helloweb 들어가면 Hello World나옴



