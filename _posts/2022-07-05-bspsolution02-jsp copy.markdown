---

layout: post
title: 'bspsolution02 - jsp'
subtitle: 'bspsolution02 - jsp'
categories: devlog
tags: bspsolution
comments: true

---
# JSP

## 데이터 속성(HTML요소)
- 형태  
    `data-속성명="속성값"`
    ```
        <div id="aaa" data-fbo="bbb" data-code="c03"></div>
    ```

- 장점  
    hidden으로 태그 숨겨두고 데이터를 저장할 필요가 없다.   
    => html 스크립트 간결해짐
- 사용하기  
    자바스크립트에서 데이터 속성을 조작하기 위한 방법은 여러개이다.
    기본적으로 DOM객체를 통해 데이터 속성 조작 가능.
    ```    
        var div = document.querySelector('#aaa');                                     
        console.log(div.dataset);
    ```

    - DOM속성으로 변환될 때 속성값은 'data-' 제외하고 실제 속성 이름을 사용
    ![image](https://user-images.githubusercontent.com/60701130/177347893-fd02ae22-f1ee-4c10-8755-7728b266fce5.png)
    `자바스크립트는 DOM 생성 시점에 "data-" 로 시작하는 속성들을 하나로 모아 "dataset" 맵(Map)으로 따로 모아서 관리`

    - 특정 속성 값 추출하기
        ```
        console.log(input.dataset.code);          
        console.log(input.dataset['code']); 
        ```
    - 데이터 속성 값 바꾸기
        ```
        var input = document.querySelector('#aaa');                                        
        input.dataset.code = 'ggg'; 
        ```