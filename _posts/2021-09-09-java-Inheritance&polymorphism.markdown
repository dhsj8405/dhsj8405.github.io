---

layout: post
title: '객체지향 상속과 다형성'
subtitle: '객체지향 상속과 다형성'
categories: devlog
tags: java
comments: true

---


# 상속과 다형성

## 상속(+upcasting,downcasting)

부모 클래스
```java
public class Person {
	private String name;
    
	public Person() {
		System.out.println("Person() called");
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
}
```
자식클래스
```java
public class Student extends Person {
	private int grade;
	private String major;

	public Student() {
		// 자식의 모든 생성자에서 
		// 부모의 특정 생성자를 명시(explicity)하지 않으면
		// 암시적(implicity)으로 부모의 기본 생성자가 
		// 자식 생성자 코드 앞에 호출된다.
		//super(); //부모클래스 생성자를 먼저 부르기때문에 super();을 밑에 프린트문의 밑에 적으면 안됨
		System.out.println("Student() called");
	}
	public int getGrade() {
		return grade;
	}
	public void setGrade(int grade) {
		this.grade = grade;
	}
	public String getMajor() {
		return major;
	}
	public void setMajor(String major) {
		this.major = major;
	}	
}
```
메인함수
```java
public class StudentTest {
	public static void main(String[] args) {
		Student s1 = new Student();
		s1.setGrade(1);
		Person p1 = s1; 	//upcasting(암시적,Implicity)
		p1.setName("둘리");		
		Student s2 = (Student)p1;	//downcasting(명시적, explicity)
		s2.setMajor("cs");	
	}
}
```

## 다형성

1. 오버로딩  
매개 변수다르고 내용 같게
2. 오버라이딩
재정의 :매개변 수 같고 내용 다르게

