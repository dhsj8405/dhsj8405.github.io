---

layout: post
title: '자바스크립트 면접질문1'
subtitle: '자바스크립트 면접질문1'
categories: study
tags: study
comments: true

---

# 자바스크립트

## this
호출에 따라 달라진다.

1. 단독 호출
    - global object, 즉 window객체에 바인딩됨
        ``` javascript
        var x = this;
        console.log(x); // window
        ```
2. 함수 안에서 호출
    - 함수의 주인(window객체)에게 바인딩됨
        ``` javascript
        var num = 0;
        function addNum() {
        this.num = 100;
        num++;
        
        console.log(num); // 101
        console.log(window.num); // 101
        console.log(num === window.num); // true
        }
        
        addNum();
        ```


## 프로토타입
프로로타입 객체 = 자바 스크립트에서 객체가 생성될 때, 생서된 객체의 부모가 되는 객체의 원형