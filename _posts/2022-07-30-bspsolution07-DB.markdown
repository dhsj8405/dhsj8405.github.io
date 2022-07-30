---

layout: post
title: '머지 - MSSQL'
subtitle: '머지 - MSSQL'
categories: devlog
tags: bspsolution
comments: true

---
# merge
update,delete,insert를 한 번에 작업 가능하다  
`머지문은 리스트 데이터를 작업할 때 유용하다고 한다.`  
=> 아마 insert,update,delete에대한 foreach문, 각각에 대한 컨트롤러,서비스 매퍼 구현에 번거로움 때문인 것같다.
```
MERGE 변경될테이블명 AS A  
    USING 기준테이블명 AS B  
    ON A.컬럼1 = B.컬럼1  
	ON A.컬럼2 = B.컬럼2  
    WHEN MATCHED THEN		//데이터가 일치한 행이 존재하지 않을 때 = 새로운 데이터 insert    
        INSERT (,,,) VALUES (,,,)    
    WHEN NOT MATCHED AND 삭제랑 구분하기위한조건식 THEN  //데이터가 일치한 행이 존재할때      
        불일치할때쿼리    
	WHEN NOT MATCHED THEN    
        불일치할때쿼리  
```
