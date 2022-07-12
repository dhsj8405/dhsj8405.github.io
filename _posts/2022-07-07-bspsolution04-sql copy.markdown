---

layout: post
title: 'bspsolution04 - sql'
subtitle: 'bspsolution04 - sql'
categories: devlog
tags: bspsolution
comments: true

---
# sql

## AES_ENCRYPT
 - 문자열을 암호화하고, 바이너리 문자열을 반환하는 암호화 기법  
 - 키 문자열 을 사용하여 문자열 값을  암호화하고 암호화 된 출력을 포함하는 2 진 문자열을 반환합니다. 
- 형태
    ```
    AES_ENCRYPT(value,key)
    ```
    value : 암호 해독할 값
    key : 문자열 데이터 유형. 
    전체 자릿수는 16자 이하
    매핑 변수를 키에 사용할 수 있다. 
    암호화할 때 사용한 키와 동일한 키를 사용하여 값을 해독

## AES_DECRYPT 
암호화된 문자열을 복호화합니다.

 ```
  SELECT AES_DECRYPT(UNHEX(필드명), '암호화 키') FROM 테이블명;
  ```

## HEX
정수값 및 문자열 값을 HEX 값으로 출력

## UNHEX
HEX로 된 값을 다시 복호화 디코딩을 수행해서 표시

## IFNULL
해당 Column의 값이 NULL을 반환할 때, 다른 값으로 출력할 수 있도록 하는 함수
```
SELECT IFNULL(Column명, "Null일 경우 대체 값") FROM 테이블명; 
```

`HEX 같이 쓰는 이유`  
VARCHAR나 CHAR, TEXT 같은 경우는 2진수로 된 데이터 타입이 아닌 문자열로 이루어진 데이터 타입 => 문자열로 이루어진 데이터 타입은 문자셋과 공백 등으로 인해 잠재적인 위험 존재

이미 TEXT나 VARCHAR 형태로 되어있는 곳은  16진수로 변환하는 함수인 HEX를 제일 앞에 붙여 사용