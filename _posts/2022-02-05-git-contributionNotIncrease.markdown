---
layout: post
title: '다른 컴퓨터에서 깃 contribution 증가 하지 않는 현상'
subtitle: '다른 컴퓨터에서 깃 contribution 증가 하지 않는 현상'
categories: devlog
tags: git
comments: true
---


# contribution 증가에 필요한 조건(공식 홈페이지)

1. 커밋한 이메일 주소(local repository의 user.email)가 깃허브 어카운트(githubl 계정의 이메일주소)와 동일/연동되어 있어야함
2. 포크한 repository에 한 commit은 카운트 되지 않음
3. repository의 기본 저장소(repository의 default branch: 보통 master) 혹은 gh-pages 브랜치에 커밋 되어야함


## 증가하지않은 이유  
로컬 깃 유저 정보가 repository에 등록되어 있지 않았다.

ex)  
유저이름 : abcd  
유저이메일 : abcd@abcd.com

```
git config --global user.name abcd
git config --global user.email abcd@abcd.com
```