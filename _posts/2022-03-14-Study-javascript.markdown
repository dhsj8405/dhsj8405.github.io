---

layout: post
title: '자바스크립트 면접질문1'
subtitle: '자바스크립트 면접질문1'
categories: study
tags: study
comments: true

---

# 자바스크립트

## 이벤트 전파
1. 캡쳐링 단계
이벤트가 있는 곳 클릭할때, Document root에서 이벤트가 발생하고 캡쳐링이 발생한다.
- 이벤트 캡쳐링 : 이벤트가 발생했을 때 상위에서 하위 요소로의 이벤트 전파 방식
2. target 단계
이벤트가 타겟 엘리먼트에 도달

3. 버블링 단계
다시 이벤트가 target부터 document root로 올라간다.
- 이벤트 버블링 : 이벤트가 발생했을 때 하위에서 상위 요소로의 이벤트 전파 방식

## 이벤트 위임(Event delegation)
하위 요소마다 이벤트를 붙이지 않고 상위 요소에서 하위 요소의 이벤트들을 제어하는 방식

장점
- 핸들러 할당이 줄어듬으로써 단순해지고 메모리가 절약
- 동적인 엘리먼트에 대한 이벤트 관리가 수월
```html
<!DOCTYPE html>
<html lang="en">
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Example</title>
</head>
<body>
    <div id="Menu">
        <button data-action="save">저장하기</button>
        <button data-action="reset">초기화 하기</button>
        <button data-action="load">불러오기</button>
    </div>
    <script src="app.js"></script>
</body>
</html>
```
``` javascript
const $Menu = document.getElementById('Menu')

const ActionFunctions = {
  save: () => alert('저장하기'),
  reset: () => alert('초기화하기'),
  load: () => alert('불러오기'),
}

$Menu.addEventListener('click', e => {
  const action = e.target.dataset.action
  if (action) {
    ActionFunctions[action]()
  }
})
```

- dataset  
dataset은 특정한 데이터를 DOM 요소에 저장할 수 있다.
데이터 속성은 'data-'로 시작해야 한다.  

    `장점`  
    \<input> 태그에 hidden으로 데이터를 숨겨두지 않아도 된다.  

    - 사용법
    1. HTML 태그에 접두어(data-)가 붙은 속성을 추가하고, 거기에 사용하고자 하는 값을 지정해놓는다.

    2. 자바스크립트에서 요소를 선택하고, dataset 객체에서 커스텀속성을 읽어들인다.(접두어는 생략)

        `dataset 속성의 값은 개수 제한이 없다`

## null, undefined, undeclared의 차이
null  
- 아무런 값도 할당하지 않았다는 것    

undefined  
- 변수가 선언되었지만, 값은 할당되지 않았다  

undeclared  
- var, let, const를 사용하지 않고 생성한 변수에 값을 할당할 때 생성된다.  


## 클로저(Closure)

이미 생명 주기가 끝난 외부 함수의 변수를 참조하는 함수
``` javascript
1 function outter(){
2     var title = 'coding everybody';  
3     return function(){        
4         alert(title);
5     }
6 }
7 inner = outter();
8 inner();
```

특성  
내부함수가 외부함수의 지역변수에 접근 할 수 있고, 외부함수는 외부함수의 지역변수를 사용하는 내부함수가 소멸될 때까지 소멸되지 않는다.

특징  
캡슐화 가능 : 자바스크립트에서 변수 또는 함수를 private처럼 쓸 수 있다

```javascript
function outter(){
    var x = 10;

    this.getX = function(){
        return x;
    }

    this.setX = function(num){
        x = num;
    }
}

var inner = new outter();
console.log(innter.getX());
console.log(innter.x)

innter.setX(20);
console.log(innter.getX());
```

## 실행 컨텍스트
실행 가능한 코드가 실행되기 위해 필요한 환경  
- 구성  
렉시컬 환경, 변수 객체(파라미터와 변수 정보), this  

브라우저가 스크립트를 로딩하면 전역 컨텍스트가 먼저 생성된 후, 함수 호출 시마다 함수 컨텍스트가 생성된다.
컨텍스트 생성 후 함수가 실행되는데, 사용되는 변수들은 변수 객체 안에서 값을 찾고 없다면 스코프 체인을 따라 올라가며 찾는다.
함수 실행이 마무리되면 해당 컨텍스트는 사라진다.
