---
title:  "[Spring] 9 - 예외처리(Exception)"
categories: Spring
tags:
  - Spring Framework web MVC Exception
toc: true
toc_label: "On this Page"
toc_icon: "cog"
header:
  overlay_image: "/assets/images/Spring/springcover.png"
  overlay_filter: 0.5
  image_description: "header cover image"
---

<br />
<br />

>> 해당 게시글의 전체 소스코드는 이곳 <a href="https://github.com/doorisopen/SpringSpring/tree/55e32924a3b2bbb9e287e7765e9d234f16d8cb4e"><strong>Github</strong></a>를 참고해 주세요

<br />

### 목차
>> 1. __예외 처리 동작 이해하기__

<br />
<br />


<hr />

### Spring MVC에서의 예외 처리
* __컨트롤러 별로 예외 처리__
  + __컨트롤러의 메서드에서 예외가 발생했을 때의 처리를 정의__
  + 별도의 예외 처리 메서드를 정의하고 그 메서드에 @ExceptionHandler 애노테이션 설정
* __하나의 웹 애플리케이션 안에서 공통된 예외 처리__
  + __복수의 컨트롤러에서 사용할 수 있는 공통된 예외 처리 클래스를 정의__
  + 공통된 예외 처리 클래스를 정의하고 그 클래스에 @ControllerAdvice 애노테이션을 설정

#### ControllerAdvice 클래스
* __@Component 설정__ 은 __component-scan__ 을 통해 빈으로 등록
* __@ControllerAdvice__ 는 예외처리 클래스임을 선언
* __@ExceptionHandler__ 는 특정 예외를 처리할 메서드임을 선언

<hr />

#### 예외 처리 설정하기
* __servlet-context.xml__

``` xml
<context:component-scan base-package="org.doorisopen.myspring.excption" />
```

* __MemberServiceImpl.java__

``` java
...
public MemberVO readMember(String id) throws Exception {
    if(memberDAO.read(id) ==  null) throw new DataNotFoundException(id);
    return memberDAO.read(id);
}
...
```

#### org.doorisopen.myspring.exception
* __MemberControllerAdvice.java 내용__

``` java
@Component
@ControllerAdvice
public class MemberControllerAdvice {

    @ExceptionHandler(Exception.class)
    @ResponseStatus(HttpStatus.INTERNAL_SERVER_ERROR)
    public String handleException(Exception e) {
    	e.printStackTrace();
        return "exception/error";
    }

    @ExceptionHandler(DataNotFoundException.class)
    public String handleException(DataNotFoundException e) {
    	e.printStackTrace();
        return "exception/not_found";
    }

}
```

* __DataNotFoundException.java 내용__

``` java
public class DataNotFoundException extends Exception {

	private static final long serialVersionUID = 1000L;

    public DataNotFoundException() {
    }

    public DataNotFoundException(String msg) {
        super(msg);
    }

    public DataNotFoundException(Throwable th) {
        super(th);
    }
}
```

* __views -> exception -> error.jsp__

``` html
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>

<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8">
	<title>Exception ERROR</title>
</head>
<body>
	예외 클래스 :	${exception.getClass().name} <br>
  	메시지 : 	${exception.message}
</body>
</html>
```

* __views -> exception -> not_found.jsp__

``` html
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>

<!DOCTYPE html>
<html>
<head>
	<meta charset="UTF-8">
	<title>DataNotFoundException</title>
</head>
<body>
	<h1>DataNotFoundException</h1>  
</body>
</html>
```

<hr />

### References
> * From by [doorisopen](https://doorisopen.github.io/)
