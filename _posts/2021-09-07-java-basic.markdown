---

layout: post
title: '객체지향 기본개념'
subtitle: '객체지향 기본 개념'
categories: devlog
tags: java
comments: true

---

**1. 서론**

# 알아두면 좋은것 (+이전시간 복습)

 ## .gitignore
 = 원격 저장소에 관리하지 말아야되는 파일 지정해주는 것
 프로그램마다 달라짐, tool에 관련된 설정이 다름 **협업에서 중요
 
파일 내용
**/.classpath
**/.project
**/.settings
**/target
**/build
파일 내용 위에 3개는 이클립스 설정파일 (git에 안 올리는 게 좋음 )

## cli (<=> gui : graphic user interface)
= command line interface  
 tip) cli 익숙해지는 게 좋음

## 깃 레포지토리 생성
- 레포지토리 네임은 프로젝트 
네임이랑 같게하는 게 팁

```
* 이부분 잘 생각안남 
레포지토리 주소 복사  
eclips)
프로젝트 - team - shareproject (= cli에서 git init과 동일한 기능)
use or create repository in parent folder of project 체크
create repository 하고 내용 체크 - finish
```
## md 파일 사용이유
md파일 = mark down(html 태그들이 너무많아서 사용)
설명용

### git에서 md파일 염탐하는방법
 md파일들어가서 raw눌리면 어떻게 만들었는지 나옴

### 이클립스에서 md 만드는법
설명하고싶은 프로젝트파일 우클릭 - new - file - readme.md 적고 생성
markdown source 에서 적기

### 임시로 보는 법
이클립스에서 preview 누르기

### readme로 자바 소스 적을 때
공백
```java
public class HelloWorld{
}
```
공백 

## 협업과정
팀원들간 맡은 서브프로젝트한것들 깃으로  커밋하고 jenkins소프트웨어에 git url 주고 세팅해주면 자동으로 빌드해줌
서버에 자동으로 보내주기도함 (배포) - 팀장은 어플리케이션 잘 돌아가는지 확인
팀장이 자기꺼에 paste 해서 에러 테스트하고 퇴근 허락다음날
아침에 출근해서 pull 해줘야함
javastudy 우클릭 team - pull

## uml
설계하는 도구 (unified modeling language)
관계들을 표현하는것

### 참고서적
* UML 실전에서는 이것만 쓴다 
링크 http://www.kyobobook.co.kr/product/detailViewKor.laf?barcode=9788991268937
객체지향 설계원칙을 가르쳐줌 

### uml 주의사항 
화살표 ( 의존성표시) 향하는 방향의 클래스가없으면 돌아가지않음 02.java ppt p6

## static
모든 객체에서 공유함 (클래스에 붙어서 로딩할때 생김 ,하나만 있는것)
