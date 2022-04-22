---

layout: post
title: 'yarn start 에러'
subtitle: 'yarn start 에러'
categories: devlog
tags: react
comments: true

---

# 에러 사진
![image](https://user-images.githubusercontent.com/60701130/164644269-7180bc4c-ed32-437b-b2c7-26754c3ed47d.png)

# 해결방법

1. wiondows powerShell 관리자 실행
![image](https://user-images.githubusercontent.com/60701130/164644589-b403d67a-4030-49f3-8a79-cbe1d8291573.png)

2. 현재 권한 상태 확인
![image](https://user-images.githubusercontent.com/60701130/164644769-e17d5a3e-7a99-4288-b288-b07570d5d345.png)
`get-ExecutionPolicy`

- 권한 상태값 

 Restricted : default설정값으로, 스크립트 파일을 실행할 수 없습니다.  
 AllSigned : 신뢰할 수 있는(서명된) 스크립트 파일만 실행할 수 있습니다.  
 RemoteSigned : 로컬에서 본인이 생성한 스크립트와, 신뢰할 수 있는(서명된) 스크립트 파일 실행할 수 있습니다.  
 Unrestricted : 모든 스크립트 실행가능  
 ByPass : 경고/차단 없이 모든 것을 실행가능하도록함  
 Undefined : 권한을 설정하지 않겠음  

3. 권한 변경해주기
![image](https://user-images.githubusercontent.com/60701130/164645212-d7d7484c-f309-49b9-b785-e0d660ec7038.png)

4. 권한 확인 후 yarn start 해보기
![image](https://user-images.githubusercontent.com/60701130/164645474-a2ce5447-c5ee-42f6-8a91-fb6dc3663e42.png)

