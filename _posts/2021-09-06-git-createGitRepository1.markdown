---
layout: post
title: '깃 로컬 레포지토리 생성1'
subtitle: '깃 로컬 레포지토리 생성1'
categories: devlog
tags: git
comments: true
---

**# 1.서론**

#  깃 관련 용어
push  
로컬레포지토리에서 깃허브에 올리는것  
pull  
깃허브에서 가져오는것 ( 로컬 브랜치에 자동으로 병합)  
fetch  
깃허브에서 가져오는것 ( 로컬 브랜치에 자동 병합 x)  

**# 2.본론**



# 로컬 깃저장소 만들기 
 ## 1. GitHub 저장소를 원격 저장소로 등록
(1) 깃허브에서 레포지토리 생성  
(2) 터미널로 메이븐프로젝트(homepractice)가 있는 폴더로이동
ex)C:\eclipse\workspace\douzone\homepractice  

```
git init  
git add -A  
git commit -m "first commit"  
git branch -M main  
git remote add origin https://github.com/dhsj8405/homepractice.git
git push -u origin main  
```

프로젝트 오른쪽 클릭 - team - share project 에서 Use or create repository in parent folder of project, (Create Repository 누르고 )하위 내용 체크  

 ## 2. git 저장위치 확인용 git perspective 생성하기(git repository)  
window - show view - other - git - git repositories 오픈
* local 레포지토리 = .git 디렉토리 

원격저장소만들기  
깃 repository의 javastudy 에서 Remotes 오른쪽 클릭 create remote - ok - change - 깃 링크 주소 넣고 Authentication에 깃의 사용자이름, 비밀번호 입력

 ## 3. gitignore 생성 (원격 저장소에 관리하지 말아야되는 파일 지정해주는 것)
네비게이터에 javastudy(maven프로젝트) 오른쪽클릭 파일생성 파일이름 .gitignore 
파일안에 ** 는 모든 디렉토리라는 뜻


 ## 4. 커밋,푸쉬하는방법1 (수업 시간에 안돼서 2번 방법으로 실행)

javastudy 최상위 디렉토리 오른쪽클릭 team -commit
- Unstaged changes 모든 파일 복사해서 staged changes에 붙여넣고
commit message에 주요 키워드 즉 , 수정이유 적기
- commit and push

* 푸쉬할 때 로그인 오류 문제 발생
  ### 해결노력 1 실패 ( cmd에서 원격저장소 생성하고 권한 부여)
cmd창에서 javastudy 폴더까지 이동후
git add -A 명령어 치기
git branch -M main
git remote add origin http~~~
git push -u origin main
치고나면 sign in with your browser 눌리기
autorize 선택하기
(위 명령어는 repository 처음 생성했을 때 메인에 적혀있음)
  ### 해결노력 2 실패
깃 설치
cmd에서 
git
git config --global user.name "dhsj8405"
git config --global user.email dhsj8405@naver.com
순서대로 실행해주기


 ## 5. 커밋,푸쉬하는 방법2(이클립스 터미널로 깃 푸쉬하기)
C:\douzone2021\eclipse-workspace\javastudy 경로로 옮기기
git add -A
git commit -m '..'           (..에 주요 키워드 즉 , 수정이유 적기)
git push