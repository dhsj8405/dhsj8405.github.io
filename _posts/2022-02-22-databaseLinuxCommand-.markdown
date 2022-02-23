---

layout: post
title: '[Linux]]db 명령어'
subtitle: '[Linux]]db 명령어'
categories: devlog
tags: --- centOS
comments: true

---

# 기본 명령어

서버에 존재하는 db 찾기  
`show database;`

db 생성  
`create database webdb;`

db 선택  
`use webdb;`

테이블 조회  
`show tables;`

테이블 생성
```
CREATE TABLE pet (  
    -> name VARCHAR(20),  
    -> owner VARCHAR(20),  
    -> species VARCHAR(20),  
    -> gender CHAR(1),  
    -> birth DATE,  
    -> death DATE );
```

테이블 상세조회  
`describe pet;`

테이블 삭제  
`drop table pet;`
