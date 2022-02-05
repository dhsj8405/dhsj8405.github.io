---

layout: post
title: '객체지향 추상 클래스와 인터페이스'
subtitle: '객체지향 추상 클래스와 인터페이스'
categories: devlog
tags: java
comments: true

---

# Ch.3-4 추상 클래스와 인터페이스

## 추상화
객체들간 공통되는 특성을 추출하는 것

## 추상 클래스
- 실체 클래스들의 공통적인 특성들을 추출해 선언한 클래스  
- 객체 직접 생성해서 사용 불가( 선언만하고 내용은 아직 추상적이기 때문)  
- 확장을 위한 용도  
- 하나 이상의 추상 메소드를 가진다 (없으면 자식클래스에 선언해야함)  
	-> 추상 메소드가 없어도 추상 클래스일 수 있음

### 문법
``` java
public abstract class 클래스명{

  //필드

  //생성자

  //메서드

}
```

### 추상 클래스 선언 및 상속

Shape(부모클래스)
```java
package com.douzone.paint.shape;

import com.douzone.paint.I.Drawable;

public abstract class Shape implements Drawable {
	private String lineColor;
	private String fillColor;
	
	public String getLineColor() {	return lineColor;}
	public void setLineColor(String lineColor) {	this.lineColor = lineColor;}
	public String getFillColor() {	return fillColor;}
	public void setFillColor(String fillColor) {	this.fillColor = fillColor;}
	
}
```
Circle
```java
package com.douzone.paint.shape;

public class Circle extends Shape {
	private int x1, y1;
	private int radius;

	@Override
	public void draw() {
		System.out.println("원을 그렸습니다.");
	}
	
	public int getX1() {return x1;}
	public void setX1(int x1) {this.x1 = x1;}
	public int getY1() {return y1;}
	public void setY1(int y1) {this.y1 = y1;}
	public int getRadius() {return radius;}
	public void setRadius(int radius) { this.radius = radius;}

}
```
Rectangle
``` java
package com.douzone.paint.shape;

public class Rectangle extends Shape{
	private int x1, y1;
	private int x2, y2;
	private int x3, y3;
	private int x4, y4;
	
	@Override
	public void draw() {
		System.out.println("사각형을 그렸습니다.");
	}
	public int getX1() {			return x1;}
	public void setX1(int x1) {		this.x1 = x1;}
	public int getY1() {			return y1;}
	public void setY1(int y1) {		this.y1 = y1;}
	public int getX2() {			return x2;}
	public void setX2(int x2) {		this.x2 = x2;}
	public int getY2() {			return y2;}
	public void setY2(int y2) {		this.y2 = y2;}
	public int getX3() {			return x3;}
	public void setX3(int x3) {		this.x3 = x3;}
	public int getY3() {			return y3;}
	public void setY3(int y3) {		this.y3 = y3;}
	public int getX4() {			return x4;}
	public void setX4(int x4) {		this.x4 = x4;}
	public int getY4() {			return y4;}
	public void setY4(int y4) {		this.y4 = y4;}
	
}
```
Triangle
```java
package com.douzone.paint.shape;

public class Triangle extends Shape {
	private int x1,y1;
	private int x2,y2;
	private int x3,y3;
	
	@Override
	public void draw() {
		System.out.println("삼각형을 그렸습니다.");
	}
	public int getX1() {	return x1;}
	public void setX1(int x1) {	this.x1 = x1;}
	public int getY1() {	return y1;}
	public void setY1(int y1) {	this.y1 = y1;}
	public int getX2() {	return x2;}
	public void setX2(int x2) {	this.x2 = x2;}
	public int getY2() {	return y2;}
	public void setY2(int y2) {	this.y2 = y2;}
	public int getX3() {	return x3;}
	public void setX3(int x3) {	this.x3 = x3;}
	public int getY3() {	return y3;}
	public void setY3(int y3) {	this.y3 = y3;}
	
}
```


## 인터페이스
- 클래스들 사이의 유사한 특성(변수,메소드)을 부자연스러운 상속 관계를 설정하지 않고 얻어냄

### 특징
- 다중 상속 가능 (+ 인터페이스 간 다중 상속 가능)  
- 인터페이스를 구현한 클래스에서 추상 메소드 반드시(인터페이스에 선언한 메소드) 정의해야 함

## Ch.3-4-6 일반클래스 vs 추상 클래스 vs 인터페이스
![](https://images.velog.io/images/dhwoo8405/post/cffed545-fde3-4fe4-ba4d-58eaa1a28fc5/image.png)
d