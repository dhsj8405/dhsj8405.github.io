---

layout: post
title: 'chat(StompJS) React & Springboot'
subtitle: 'chat(StompJS) React & Springboot'
categories: devlog
tags: react
comments: true

---

`CORS-practice로 웹팩,바벨 설정먼저하고 하기`

# 사전 설치  
# webpack-practice 복사해서 사용

- package.json 생성  
`npm init -y`  

- 웹팩 라이브러리,로더, 바벨로더 설정  
 `npm i -D webpack webpack-cli webpack-dev-server babel-loader style-loader css-loader sass-loader node-sass @babel/core @babel/cli @babel/cli @babel/preset-env @babel/preset-react`    
 - react dom 사용  
  `npm i react react-dom`
 - yarn 설치  

`npm install -g yarn`
-  axios 설치  
`yarn add axios`

- stomp 모듈, socketJS 추가  
`yarn add @stomp/stompjs sockjs-client`

# CORS
react port 3000  
spring port 9099

## Server(Back)
<pre>
com.douzone.chat  
    --- ChatApplication.java  
    --- MainController.java  
    --- StompController.java    
    --- config  
        --- FilterConfig.java  
        --- SocketConfig.java  
    --- dto  
        --- ChatMessageDto.java  
        --- ChatRoomDto.java  
    --- filter  
        --- CorsFilter.java  
</pre>

메세지 전송시(client.send) 오류 
![image](https://user-images.githubusercontent.com/60701130/157266519-6b7220e9-6c54-417f-b9d3-4f0c45d795de.png)

해결
: 메시지 전송할때마다 connect해줌





