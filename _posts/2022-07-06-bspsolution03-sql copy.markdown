---

layout: post
title: 'bspsolution03 - sql'
subtitle: 'bspsolution03 - sql'
categories: devlog
tags: bspsolution
comments: true

---
# sql

## case when then 표현식
예시
```
SELECT
 CASE
  WHEN '조건' THEN '조건에 만족할 때 출력할 데이터'
  ELSE '조건에 만족하지 않을 때 출력 데이터'
 END
FROM 테이블;
```

## count(1) 
 전체 행 개수
 = count(*)

## concat

컬럼 데이터와 컬럼 데이터를 연결합하여 하나의 스트링 문자열로 표시

![image](https://user-images.githubusercontent.com/60701130/177559093-850ad264-4cf1-4853-b2f6-99afe792631e.png)


![image](https://user-images.githubusercontent.com/60701130/177559146-c1d776ae-c074-4a55-9c90-f95954e35779.png)


## group_concat

특정컬럼의 각 결과값을 하나의 가로열(ROW)로 표시합니다.

![image](https://user-images.githubusercontent.com/60701130/177559218-da50c04e-875a-4e53-bc08-9d26df87b9e9.png)

