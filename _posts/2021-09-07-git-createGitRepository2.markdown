---
layout: post
title: '깃 로컬 레포지토리 생성2'
subtitle: '깃 로컬 레포지토리 생성2'
categories: devlog
tags: git
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

### git에서 md파일 작성 방법 확인하기

 md파일들어가서 raw눌리면 어떻게 만들었는지 나옴

### 이클립스에서 md 만드는법
설명하고싶은 프로젝트파일 우클릭 - new - file - readme.md 적고 생성
markdown source 에서 적기

### 이클립스에서 md 파일 미리보기  
md 파일 밑에 preview 누르기

### readme로 자바 소스 적을 때

`형식`

&#96;&#96;&#96;java  

자바 문법

&#96;&#96;&#96;

`결과`
```java
public class HelloWorld{
}
```

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

--- 

**2. 본론**

# 깃 저장소
## 깃허브  토큰 생성 (ex:api 쓸때)
자신 깃허브 프로필 클릭 -  settings - developer settings - personal access tokens - generate a personal access token  
토큰네임 지정후 만료기간 설정
밑에 권한 전부 체크하기  
----- 결과 -----  
personal access tokens  ( 토큰은 까먹으면 귀찮음)  
**Make sure to copy your personal access token now. You won’t be able to see it again!
= ~~~~(토큰)

## 깃 로컬 레퍼지토리 삭제 방법
  깃 퍼스펙티브 우클릭 - delete repository - 첫번째 항목 (Delete Git repository data and history)만 체크
  
## 깃 레포지토리 삭제 방법
레포지토리 settings - 맨밑에 delete - 깃아이디/레포지토리name 입력

## 이클립스에서 깃 레포지토리 깃 로컬 레포지토리 연결작업(gui방식)
이클립스에서 깃 레포지토리 remotes에 마우스 오른쪽 클릭 - create remote - configure fetch 선택후 create
-change - git url입력 - 밑에 user에 git사용자이름 , 패스워드에 깃 토큰에서 발급받은 번호

## 이클립스로 git에 올리는법 = Git staging(git add -A)
올리려고하는 프로젝트 우클릭 - team - commit 하고 git staging 탭 가서 Staged Changes 에 올리고
commit message에 키워드 내용 써주기 (git commit -m "first commit")
push and fetch 버튼 -preview - push

## push
연결된 github에 올리는것
## pull 
git에서 가져오는 것
## commit
원본을 로컬 깃저장소에 저장하는것 
## fetch
원격 저장소에서 로컬 깃저장소에 즉, 로컬에 가져오기만 하는 것





## 남의 코드, 프로젝트 clone하는 방법
누군가 만든 기초 프로젝트 (라이브러리 테스트도 한것 = guide를 주는것임)
=> 기초프로젝트 만드는사람 software architect 역할(부장님)

### pull
clone 하려는 프로젝트가있는 깃 저장소의 code버튼 선택 - 깃 url 카피
git 퍼스펙티브 아무곳 누르고 붙여넣기 - next - next - directory는 워크스페이스폴더 지정

### 프로젝트 등록 import 과정
import하려면 maven으로 프로젝트 만들어야함
.settings
.classpath
.project
가 포함된파일 =  이클립스 프로젝트
### 임포트작업
깃의 메이븐 프로젝트를 읽어서 pom.xml을 읽고 이클립스 프로젝트로 변경하는 과정
워킹트리 오른쪽 - import project - finish

