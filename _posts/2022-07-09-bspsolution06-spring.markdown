---

layout: post
title: 'bspsolution06 - spring'
subtitle: 'bspsolution06 - spring'
categories: devlog
tags: bspsolution
comments: true

---
# spring

## 모델 객체에 쓰이는 어노테이션
 
- @JsonFormat(shape = JsonFormat.Shape.STRING, pattern = "yyyy-MM-dd HH:mm:ss")
Jackson 라이브러리에서 제공하는 어노테이션, JSON 응답값의 형식을 지정할 때 사용한다

- @JsonDeserialize(using = LocalDateTimeDeserializer.class)
	Json 데이터를 Java 객체로 변환
	```
		@JsonDeserialize(using = "내가 정의한 deserializer")
	```

- @JsonSerialize(using = LocalDateTimeSerializer.class)
	Java 객체를 Json 데이터로 변환