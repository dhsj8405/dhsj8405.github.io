---

layout: post
title: 'redis세팅'
subtitle: 'redis세팅'
categories: devlog
tags: redis
comments: true

---

# Redis
인 메모리 데이터베이스
- 캐시 시스템
- 영속성  
    데이터를 생성한 프로그램의 실행이 종료되더라도 사라지지 않는 데이터의 특성   
- 다양한 자료구조  
    개발 편의성 좋아지고 난이도 낮아진다.
# Redis 설치
[redis 설치](https://github.com/microsoftarchive/redis/releases)

- redis 서버 실행  
 redis-server.exe 실행
- cli로 확인하기  
 redis-cli.exe 실행
 ![image](https://user-images.githubusercontent.com/60701130/166664129-9669b46d-3143-4fc1-862f-e37aa9c37a15.png)

# spring boot 연동하기

1. 의존성 추가하기
    - pom.xml
        ```
        <dependency>
                    <groupId>org.springframework.boot</groupId>
                    <artifactId>spring-boot-starter-data-redis</artifactId>
            </dependency>
        ```
2. yml 환경설정
    ```
    spring:
    redis:
        lettuce:
        pool:
            min-idle: 0
            max-idle: 8
            max-active: 8
        port: 6379
        host: localhost
    ```


# 에러
1.java.util.zip.ZipException: invalid LOC header
- 해결방법  
.m2/repository 안의 라이브러리들 전부 삭제하고 다시 메이븐 업데이트 

2. regeneratorRuntime is not defined  
async await 사용시 에러발생
커맨드 설치
    ```
    > npm install --save-dev @babel/plugin-transform-runtime
    > npm install --save @babel/runtime
    ```
    - 바벨 설정
    ```
    {
    "plugins": ["@babel/plugin-transform-runtime"]
    }
    ```