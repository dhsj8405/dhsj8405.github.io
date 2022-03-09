---

layout: post
title: '[Linux]]db 권한부여 및 윈도우 워크벤치 연결'
subtitle: '[Linux]]db 권한부여 및 윈도우 워크벤치 연결'
categories: devlog
tags: --- centOS
comments: true

---

# mariadb-데이터베이스-사용자-생성- 권한부여

0. DBA 권한으로 접속
`mysql -u root -p`

1. database 생성  
MariaDB [none]> `create database webdb`;  

2. user 생성  
MariaDB [none]> `create user 'webdb'@'192.1xx.xxx.xxx' identified by 'webdb'`;    
=> create user '유저명'@'hostname' identified by '패스워드명';  

3. 권한 부여
MariaDB [none]> `grant all privileges on webdb.* to 'webdb'@'192.1xx.xxx.xxx'`;  
=> grant all privileges on db명.* to '유저명'@'hostname  

4. 새 변경사항 적용  
MariaDB [none]> `flush privileges`;  

4-1. 사용자별 권한 조회
`show grants for '사용자계정'@'호스트';`

5. Windows의 Workbench 에서 테스트 

![image](https://user-images.githubusercontent.com/60701130/155357161-5007593a-4c9d-43ca-b90b-367060d9ff58.png)
- 위 사진은 에러 해결 후 사진임


에러 뜸

![image](https://user-images.githubusercontent.com/60701130/155358262-34f63c9e-4841-442f-a62d-e3173a63f4e8.png)

원인
1. 바보같이 포트번호에 ssh포트번호인 22번 넣고있었음
2. mysql포트는 기본적으로 3306인데 왜그런지 모르게 3307로 돼있었음

해결  
-  port번호에 mysql에 할당된 포트번호를 넣어야함   
- 포트 번호 확인방법  
    `netstat -tulpn | grep LISTEN`

testconnection 누르고 성공하면 ok

