---
layout: post
title: '자바 개발환경 구축'
subtitle: '+ maven 멀티프로젝트생성'
categories: devlog
tags: java
comments: true
---

**# 1.서론**
# 알고있으면 편하고 좋은것
●프로젝트 네임은 소문자 (중요한 관례 !)  
●패키지 네임: 소문자 (회사 이름은 거꾸로)(com.douzone.프로젝트네임)  
●javac파일 위치
C:\Program Files\Java\jdk1.8.0_301\bin

# 자바 빌드과정
 ## 1. jar
src (.java파일)을 컴파일하면 class  그걸 패키징하면 jar  
scr(java, 패키지)   scr까지가 물리적인 경로  
 = 과정 (build)

 ## 2. war 
web 은 class들을 war로 묶어야함 (jar에서 클래스에 html,css 이 추가)

# build tool 종류
ant  
maven * 수업 때 쓰임   
gradle  

# java perspective 추천
1. 웹할땐 javaee  
2. 콘솔 java
# 라이브러리 사용방법
project의 property - java build path - library에 등록
# Native project
 ## 1. 이클립스 Native project
  ### 형태
/helloworld[Eclipse Native Project]  
	---- src  
	---- bin  
	---- .project  
	---- .classpath  
	---- /.settings  

컴파일하면 src의 com/douzone이 bin 폴더에도 생기면서 H.class 가생김  
깃허브에 위의 bin, .project, .classpath, /.settings는 올리면 안됨  
( 해결법 : build tool로 해결 
   = maven프로젝트에 .gitignore생성
   = 본론 깃저장소 만들기 3에있음 )
build tool이 Native intellij와 eclipsed의 호환을 가능케함

#  깃 관련 용어
push  
로컬레포지토리에서 깃허브에 올리는것  
pull  
깃허브에서 가져오는것 ( 로컬 브랜치에 자동으로 병합)  
fetch  
깃허브에서 가져오는것 ( 로컬 브랜치에 자동 병합 x)  

 ## 2. Intellij Native project
  ### 형태
/helloworld[Intellij Native Project]	네이티브 이클립스 디렉토리와 호환이 안됨  
	---- /.idea  
	---- src  
	---- traget  

maven파일 구성  
src/main/java  
src/text/java  
src/main/resource  
pom.xml  
maven을 이클립스나 인텔리제이에  임포트하면 호환됨  


**# 2.본론**



# 개발환경구축
# 1.환경변수 설정
내 컴퓨터 - 시스템속성 - 고급 시스템 설정 - 환경변수 - 시스템 변수의 path 편집 - 새로만들기 - jdk파일의 bin폴더 경로 넣기
# 2.이클립스 깔고 해야하는 설정
1. window - preferences - encoding 검색 - content Types - text안에 java properties file 빼고 각각 파일의 defalut encoding 에 UTF-8업데이트해주기 
2. window - preferences - encoding- general - workspace 맨밑에 other - utf-8 선택(Text file encoding)
3. window - preferences - encoding에 web,xml 하위에 files들 엔코딩방식 utf-8로바꾸기
4. window - preferences - spelling 검색해서 spelling 맨위 체크 없애기 (Enable spell checking)
5. window - preferences - java - installed JREs  add 해서 jdk 우리걸로바꿔주기 


# maven 멀티 모듈 프로젝트 만드는법
 ## 1. maven 프로젝트 부모관계
/parent(프로젝트)  
	---- child1(모듈)	모듈간 라이브러리 의존성 존재함  
	---- child2  
  

 ## 2. 생성
file -new - project - maven - maven prject - create a simple project(체크) - next  
ex)
group id : com.douzone
artifact id : javastudy
packaging은 pom 체크 (부모가 폼이 돼야하기 때문)
* 부모는 src 폴더 없어도 됨 (삭제하기)


 ## 3. maven 업데이트 방법
maven은 바꾸고나면 update maven project 해줘야함 (단축키 : Alt F5)

 ## 4. maven 폼으로 라이브러리 적용하는 방법
구글에 maven mariadb jdbc 치고 소스 복사해서 pom의 dependencies 태그 사이에 붙여넣기 
  ### 업데이트 후 다운로드된 라이브러리위치
C:/사용자/user/.m2/repository


## 5. maven으로 프로젝트실행하기 (빌드하는것)
pom.xml오른쪽버튼 - run as - maven build 



 ## 6. 자식 모듈 만드는 방법
자식은 프로젝트 추가 메이븐 모듈생성  
멀티 모듈을 가질 프로젝트 우클릭 - new -project- Maven - MavenProject  
create a simple project 체크 -모듈네임 (ex:project1) next  
ex)
group id : com.douzone