---

layout: post
title: 'bspsolution01 - jsp,mybatis'
subtitle: 'bspsolution01 - jsp,mybatis'
categories: devlog
tags: react
comments: true

---
# JSP

## dataTable
jQuery JavaScript 라이브러리를 위한 플러그인  
=> 빠르게 게시판 보드 구현가능하게하는 라이브러리

### 속성
 searching: false      // 검색 기능 숨기기  
 ordering : false      // 정렬 기능 숨기기  
 paging: false         // 페이징 기능 숨기기  
 processing            // 서버측 처리를 위한 테이블 처리 중일 때 '처리중'이라는 표시를 띄움  
 =>대량의 데이터 테이블에서 유용(ex:항목정렬시)  
 serverSide            // 서버 측 처리를 위해 사용  
 => 데이터처리가 많아질 때 서버 처리가 좋음

`주의할 점`  
- .dataTable();  
    반환값 : jQuery 오브젝트  
- .DataTable();  
    반환값 : DataTable의 API 오브젝트  

# mybatis
## resultMap

```
    //resultMap 복잡한 결과 매핑시 사용
    // - id : resultMap의 아이디
    // - type : resultMap의 자료형(=resultType)
    <resultMap id="baseResultMap" type="Comment">
        // id: 구분자역할을 하는 속성(기본키)
        <id column="comment_no" jdbcType="BIGINT" property="commentNo"/>                    
        // result: 일반 속성 column(table)을 property(객체)에 매핑하는 느낌
        <result column="user_id" jdbcType="VARCHAR" property="userId" />                    
        // column 테이블의 컬럼명
        // jdbcType : 테이블의 자료형
        // javaType : 자바의 자료형
        // property : 자바의 속성명
        <result column="reg_date" jdbcType="TIMESTAMP" property="regDate" />
        <result column="comment_content" jdbcType="VARCHAR" property="commentContent" />
    </resultMap>
    <select id="selectCommentByPrimaryKey" parameterType="Long" resultMap="baseResultMap">
        SELECT comment_no, user_id, comment_content, reg_date FROM tcomment
        WHERE comment_no = #{commentNo}
    </select>
```

## collection
1:N 관계의 테이블을 조인할 때 사용 (조인 객체)
ex) 1개의 Comment에는 M개의 Reply가 존재
- property : 조인객체명 
- ofType : collection의 자료형(제네릭)

    ```
      private List<Reply> replies;
    ```

    ```
        <resultMap id="collectionResultMap" type="Comment">
        <id column="comment_no" jdbcType="BIGINT" property="commentNo"/>
        <result column="user_id" jdbcType="VARCHAR" property="userId" /> 
        <result column="reg_date" jdbcType="TIMESTAMP" property="regDate" />
        <result column="comment_content" jdbcType="VARCHAR" property="commentContent" />
        <collection property="replies" ofType="Reply">
            <id property="replyId" column="reply_id"/>
            <result property="userId" column="user_id"/>
            <result property="replyContent" column="reply_content"/>
            <result property="regDate" column="reg_date2"/>
        </collection>
    </resultMap>
    <select id="selectCommentByPrimaryKeyCollection" parameterType="long" resultMap="collectionResultMap">
        SELECT c.comment_no, c.user_id, c.comment_content, c.reg_date, r.reply_content, r.reg_date AS reg_date2 FROM tcomment c, reply r
        WHERE c.comment_no = r.comment_no AND c.comment_no = #{commentNo}
    </select>
    ```

## constructor 
생성자를 통한 맵핑, 생성자 파라미터에 명시된 순서대로 arg를 입력해야함
```
    <resultMap id="constructorResultMap" type="Comment">
        <constructor>
            // idArg : 구분자역할의 속성(기본키) / arg : 일반 속성
            <idArg column="comment_no" javaType="long"/>
            <arg column="user_id" javaType="string"/>
            <arg column="reg_date" javaType="date"/>
            <arg column="comment_content" javaType="string"/>
        </constructor>
    </resultMap>
    <select id="selectCommentByPrimaryKey" parameterType="Long" resultMap="constructorResultMap">
        SELECT comment_no, user_id, comment_content, reg_date FROM tcomment
        WHERE comment_no = #{commentNo}
    </select>
```

## association
1:1 관계의 테이블을 조인할 때 사용 (조인 객체)
ex) 1개 Comment 에는 1명의 User만 존재
  - property : 조인객체명 / javaType : 조인객체의 자료형

```
    private User user;
```

```
    //자바빈파일의 자료형=javaType(User), 객체명=property(user) 일치
    <resultMap id="associationResultMap" type="Comment">
        <id column="comment_no" jdbcType="BIGINT" property="commentNo"/>
        <result column="user_id" jdbcType="VARCHAR" property="userId" />
        <result column="reg_date" jdbcType="TIMESTAMP" property="regDate" />
        <result column="comment_content" jdbcType="VARCHAR" property="commentContent" />
        <association property="user" javaType="User">
            <id property="userId" column="user_id"/>
            <result property="userName" column="user_name"/>
        </association>
    </resultMap>
    <select id="selectCommentByPrimaryKeyAssociation" parameterType="long" resultMap="associationResultMap">
        SELECT c.comment_no, c.user_id, c.comment_content, c.reg_date, u.user_name FROM tcomment c, tuser u
        WHERE c.user_id = u.user_id AND comment_no = #{commentNo}
    </select>
```