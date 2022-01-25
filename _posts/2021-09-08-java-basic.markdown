---

layout: post
title: '객체지향 기본개념2'
subtitle: '객체지향 기본개념2'
categories: devlog
tags: java
comments: true

---

# [서론]

# 알고있으면 좋은것 

## 리터럴 
값(문자)을 그대로 표현하는것 

## 클래스
구조 
헤더,필드,메소드,생성자
필드 : 필드 내용들을 데이터로 객체가 가짐

## 패키지 
공통적인 일들의 클래스들 묶은것

## print 는 int 배열 출력 바로 못함 
Arrays.toString(배열변수); 사용 (impot java.util.Arrays; 해줘야함)  
toString 객체 역할을하지만 객체아니어서 오버라이딩 불가

## toString
객체안의 데이터를 스트링으로 바꿔주는것

## this
자기 참조  
한 생성자에서 다른 생성자 호출할 때 사용
메소드 호출을 받는 객체를 의미

## string 특징
s1 = "hello"  
s2 = "world"  
s3 = s1 + s2 된다.  

## final 특징
final `변수` : 정의 다시 못함 = 값 대입 더 이상 못함 (다른언어의 상수와 비슷함)  
final `method` : 재정의 불가  
final `class` : 상속할 수 없다.  
ex) public static final int countOfGoods = 0;
파이널 변수는 대문자로 적어주는 게 좋음(일반 변수는 소문자)

## 자바 실행 cli명령어 
java -cp 패키지명.클래스명 

## class 특이 용도
전역함수에 접근하기위한 네임스페이스로 사용되기도함
classname.main()
- 네임 스페이스 : 이름을 구분 할 수 있게 해주는 공간을 의미

## 객체 초기값 세팅
 null 값 대입(변수는 int a = 0;)

## call by value 
리터럴값

## call by reference
referece value
address

## swap
call by reference 객체로 넘겨야 swap 함수 구현가능  
컴파일러는 파라미터 변수가 우선이어서 오른쪽 변수에 대입  
```java
public class Value {
	private int val;
	
public Value( int val) {
		this.val = val; // this.val(인스턴스 변수)  = val(파라미터)
	}
}
```


```java
public class SwapTest03 {
	public static void main(String[] args) {
		Value a = new Value(10); // [ex) 레퍼런스값 1000] 이 a에 들어감 레퍼런스 1000이 heap영역의 val = 10 을 가리킴
		Value b = new Value(20);
		System.out.println(a.val + ":" + b.val);
		/* swap하기*/
		swap(a,b);
		System.out.println(a.val + ":" + b.val);
	}
	public static void swap(Value p, Value q) {
		int tmp = p.val;
		p.val = q.val;
		q.val = tmp;
	}
}
```



## 메모리 구조

### 스레드
하나의 프로세서에서 각 독립적인 일의 단위  
= 각 작업을 스레드화해서 병렬적으로 작업을 처리(멀티스레딩)할 수 있어야함  

`특징` code,data,heap영역 공유  

<span style="color:red">stack을 독립적으로 할당하는 이유(스레드 특징에서 stack 공유 안하는 이유)</span>  
: 실행 흐름을 추가하기위해(멀티스레딩을 위함)

스택 메모리 공간이 독립적이라면, 독립적인 함수 호출이 가능하다  
= 독립적인 실행 흐름(함수 실행)이 추가되는 것이다.
결과적으로 실행 흐름 추가(멀티스레딩)를 위해 



### 프로세스
실행중인 프로그램 (크롬 브라우저 2개면 프로세스 2개 => 하나의 어플리케이션으로 다중 프로세스 만든것)  
- 멀티 프로세스  
엑셀,워드 둘중에 하나가 오류 생겨도 나머지는 여전히 사용가능

`특징` 완벽히 독립적: 메모리 영역(code,data,heap,stack)을 다른 프로세스와 공유 하지 않음  
이유: 어플리케이션 실행시 운영체제가 각 프로세스에 메모리를 할당해서 실행하기 때문


### stack (LIFO)
지역 변수(메소드 내에서 선언된 변수들),  
매개변수(메소드 파라미터)가 저장된다.
메소드가 호출될 때 메모리에 할당되고 종료되면 메모리가 해제됨  
`특징` 선언된 블록 안에서만 유효

### heap
new 키워드를 통해 생성되는 객체,  
배열,스트링들이 저장된다.


#### 스트링 생성방식에 따른 차이  

![image](https://user-images.githubusercontent.com/60701130/150914424-330ad15d-60de-420b-ab42-7a82e52758f0.png)  
![image](https://user-images.githubusercontent.com/60701130/150914904-f9f6f8c6-f0f1-451c-820c-50dce86b4f71.png)

|생성방식|new|리터럴|
|:---|:---|:---|
|저장 장소|heap영역|heap(string pool)|
|동장 방식|같은 문자열 존재해도 다른 주소 반환 |string pool에 "strByLiteral" 문자열을 해싱한 해싱 값(hashCode)가 있으면 해당 주소값 반환, 그렇지않으면 hashCode를 저장하고 새로운 주소값 반환|
|동일한 문자열 비교시|.equals로 비교해야 true|==으로 비교해야 동일성, 즉 두 객체의 주소까지 같은지 알 수 있다. |  

![image](https://user-images.githubusercontent.com/60701130/150916649-3281be62-9a9c-4e6c-afa5-fbcd89d59219.png)

메모리를 아끼려고 상수풀 사용하는 것  
= <span style="color:red">리터럴로 생성하는게 좋음<span>


# [본론]
# 01. 객체지향 언어 주요 개념
## 1) 클래스 정의
### a) 클래스 구조
```java
public class Car {	// 클래스 헤더
 
    private String name; 	//필드
    private int speed;		//필드
		
    //public Car{}			//생성자    
    
    public void setName( String name ) {	//메소드
        this.name = name;  
    }
    public String getName() {
         return name;	
    }
}
```
### b) 접근자
객체에있는 필드, 생성자,메소드의 접근을 제한하기 위해 사용(클래스에서도 쓸 수있음)
사용이유 : 캡슐화,정보은닉을 위한 방법
private,protected,public( 안붙이면 default)
#### (1) public
접근 제한이 없다.
메소드에서 많이사용
#### (2) protected
적용 대상 : 같은 패키지에서 접근이 가능 , 상속시 다른패키지 접근
클래스는 다른 패키지의 클래스도 상속가능하므로 다른 패키지 클래스를 상속했을때도 접근가능
클래스 생성시 superclass - broswer - choose a type에 "상속할페키지네임." 치면 목록 나옴
사용이유 : 누군가를 자식에서 쓰고 싶을 때(상속)

#### (3) default 
적용 대상 : 같은 패키지에서만 접근이 가능하다.
잘 안쓰는이유 : 다른 클래스의 것들을 자주 참조하기때문에 같은 클래스내의 것들을 잘 안씀

#### (4) private
적용 대상 : 같은 클래스에서만 접근이 가능하다.
필드에서 많이쓰임

### c) 클래스 변수, 인스턴스 변수, 지역변수

구조
``` java
class Variables{
	int i;		// 인스턴스변수 :  인스턴스 생성 후, ‘참조변수.인스턴스 변수명’으로 접근
	static int cv; //클래스변수 : ‘클래스이름.클래스변수명’으로 접근
void method(){
	int lv = 0 ; 	//지역변수
	}
}
```
클래스 변수 공유변수 사용하고 접근자 실습


https://github.com/dhsj8405/javastudy/blob/master/chapter03/src/main/java/chapter03/GoodsApp.java
```java
package chapter03;

public class GoodsApp {

	public static void main(String[] args) {
		Goods goods = new Goods();
		goods.setName("Nikon");			
		goods.setPrice(2000);
		goods.setCountStock(10);
		goods.setCountSold(20);
		goods.showInfo();

	
		goods.setPrice(-1);
		int discountPrice = goods.calcDiscountPrice(50);
		System.out.println(discountPrice);
		
		System.out.println(Goods.countOfGoods);
		Goods goods2 = new Goods();
		Goods goods3 = new Goods();
		System.out.println(Goods.countOfGoods);

		Goods2 goods4 = new Goods2(); // 클래스 변수 접근 확인용

	}

}
```

https://github.com/dhsj8405/javastudy/blob/master/chapter03/src/main/java/chapter03/Goods.java
```java
package chapter03;

public class Goods {
	public static int countOfGoods = 0 ;
	//클래스 변수는 public 을 붙이면 같은 프로그램 내에서 어디서든 접근할 수 있는 전역 변수가 됩니다.
	private static int totalCount = 0;

	private String name;
	private int price;
	private int countStock;
	private int countSold;
	
	public Goods() {
		countOfGoods++;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public int getPrice() {
		return price;
	}
	public void setPrice(int price) {
		if(price<0) {
			return;
		}
		this.price = price;
	}
	public int getCountStock() {
		return countStock;
	}
	public void setCountStock(int countStock) {
		this.countStock = countStock;
	}
	public int getCountSold() {
		return countSold;
	}
	public void setCountSold(int countSold) {
		this.countSold = countSold;
	}
	public void showInfo() {
		System.out.println(
				"name:" + name +
				" , price:" + price+
				", countStock:" + countStock+ 
				", countSold:" + countSold);
		
	}
	public int calcDiscountPrice(int percentage) {
		
		return price * percentage / 100;
	}

	
}
```

```java
package chapter03;

public class Goods2 {
	public Goods2() {
		System.out.println(Goods.countOfGoods); // 전역변수 countOfGoods 값인 3이 출력됨	
		System.out.println(Goods.totalCount);	// 에러 : private 변수는 같은 클래스 내에서만 유효
	}
}
```


### d) 메소드
#### (1) 메소드 반환
 1개 밖에 못함
 

#### (2) 메소드 이름 규칙 ***외워야함***
대/소문자,숫자,_,$ 조합하여 가능 ( 숫자로 시작 불가)

#### (3) getter, setter 메소드
필드는 private로 하여 객체 내부의 정보를 보호하고(정보은닉) 필드에 대한 Setter와
Getter를 두어 객체의 값을 변경하고 참조하는 것이 좋다.

#### (4) 인스턴스 메소드
인스턴스 변수는, 클래스변수 접근가능
인스턴스 메소드에선 인스턴스 메소드도 불러오기가능 (아무거나 다됨)

#### (5)클래스(static) 메소드
static 변수, static 메소드만 접근가능
인스턴스 변수 접근 불가
인스턴스 메소드 접근 불가
 
| <span style = "color:red">인스턴스 메소드는 Static(변수,메소드) 접근도 되고,  
클래스 메소드는 Static(변수,메소드)만 접근된다.</span>

사용 목적 : 순수함수 만들때 사용
- 순수함수(유틸함수)
바깥의 데이터를 사용하지않음
예) y = f(x) :  순수함수 아님
예) max(x1,x2); , parseInt("10");
입력파라미터만받아서 내부에서 작업 후 리턴

클래스 메소드 실습
https://github.com/dhsj8405/javastudy/blob/master/chapter03/src/main/java/chapter03/ArrayUtilTest.java
https://github.com/dhsj8405/javastudy/blob/master/chapter03/src/main/java/chapter03/ArrayUtils.java

#### (6)생성자
```java
public  class Goods {
     public Goods() {	//생성자 : 리턴값이 없다, 하지만 void를 쓰지 않는다.
          // 초기화 코드     
     }

     public Goods( String name, int price ) {

           // 초기화 코드
     }
}
```
생성자 오버로딩 
- 오버로딩 된 생성자  중복 줄이는 방법
```java
	public Song(String title, String artist) {
		//this.title = title;
		//this.artist = artist;
		// some code..
		this(title,artist,null,null,0,0);//생성자 호출하는 방법
	}
	
	public Song(String title, String artist, String composer, String album, int year, int track) {
		this.title = title;
		this.artist = artist;
		this.composer = composer;
		this.album = album;
		this.year = year;
		this.track = track;
		// some code.. 
	}
```

메소드 오버로딩
```java
	public void show() {
		System.out.println("점[x="+ x + ", y= "+ y +"]을 그렸습니다.");
	}
	public void show(boolean visible) {
		if(visible) {
			//System.out.println("점[x="+ x + ", y= "+ y +"]을 그렸습니다.");	
			show();
		}else {
			System.out.println("점[x="+ x + ", y= "+ y +"]을 지웠습니다.");
		}
```

클래스와 다형성 실습
문제
![](https://images.velog.io/images/dhwoo8405/post/a68ce90c-1cdd-4f98-8536-0b69ae886c9e/image.png)
풀이
https://github.com/dhsj8405/javastudy/tree/a6c970ca8ccec35ed1e98c12b70cbb53209949cd/practice03/src/main/java/tv