---

layout: post
title: 'Singleton Pattern'
subtitle: 'Singleton Pattern'
categories: devlog
tags: stomp
comments: true

---

# Singleton Pattern(싱글톤 패턴)

1. 인스턴스가 프로그램 내에서 오직 하나만 생성된다
2. 프로그램 어디에서든 이 인스턴스에 접근이 가능해야한다
두가지를 지키는 디자인 패턴

```
public class SingleObj {
    // 클래스내에서만 조작가능하고 범위는 전역적
    private static SingleObj 
    singleInstance = null;

    private SingleObj(){ }


    public static synchronized SingleObj getInstance(){
        if( singleInstance == null ){
            singleInstance = new SingleObj();
        }

        return singleInstance;
    }
}
```


장점
- 메모리 낭비 방지
- 속도 이점 (이미 생성된 인스턴스 활용) 
- 다른 클래스간 데이터 공유 쉬움 ( 싱글톤 인스턴스가 전역으로 사용되기때문)

단점
- 다른 클래스들에서 하나의 인스턴스를 사용하면서 결합도가 높아진다(객체지향 설계원칙인 개방-폐쇄 원칙위배)
=> 수정,테스트가 어려워짐

- 멀티스레드환경에서 동기화처리안하면 인스턴스가 두개 생성됨 (synchronized 키워드 사용해야함)

- 자원을 공유하기때문에 테스트시 매번 인스턴스 상태를 초기화 해야함


* 꼭 필요한 경우가 아니면 지양해야한다함