---
title: /Spring/ AOP, Interceptor, Filter
author: ggggraceful
date: 2023-02-04
categories: [03.STUDY, Spring]
tags: [study, spring]
---

<br/>
<br/>

# AOP, Interceptor, Filter

---

웹 개발을 하다 보면 실제 비즈니스 로직이 호출되기 이전, 이후에 공통적으로 처리해야 할 기능들이 존재하는데  
대표적인 예로 Logging, 인증, 인가, 인코딩 변환 등등이 있다.  

공통적인 기능의 코드를 모든 모듈 및 페이지에서 작성하게 되면   
코드의 중복이 발생하게 되고 MSA 기반에서는 각 모듈마다 다른 코드가 작성되어 관리가 힘들 수 있다.  

따라서 공통 기능을 모아서 처리 할 수 있는 방법으로 이 세가지가 사용된다.  

하지만 이 세가지는 약간의 차이점이 존재하는데 우선 호출되는 시기가 다르다.

<br/>
<br/>

- ***Filter***
  - 일반적으로 스프링과 무관하게 전역적으로 처리해야 하는 작업들을 처리할때 사용
  - Spring이 실행 되기전 실행되며, 톰캣과 같은 웹컨테이너(WAS)에서 처리 해줌
  - Request / Response에 대한 조작이 가능
  - HTTP 프로토콜로 들어오는 모든 요청을 가장 먼저 받아 처리
  - (사용)
    - 공통된 보안 및 인증/인가 관련 작업(XSS방어)
    - 이미지/데이터 압축 및 문자열 인코딩 변환 처리
    - Spring과 분리되어야 하는 기능
    - 모든 요청에 대한 로깅

<br/>

- ***Interceptor***
  - 로그인 체크, 권한체크, 프로그램 실행시간 계산작업 로그확인 등의 작업
  - Dispatcher Servlet에 N개 등록 될 수 있음(DS가 해당 요청을 처리 가능한 Intercepter에게 할당)  
  - 스프링의 모든 빈 객체에 접근 가능
  - (사용)
    - 세부적인 보안 및 인증/인가 공통 작업( 특정 사용자는 특정 기능을 사용 못하게 막음)
    - API 호출에 대한 로깅
    - Controller로 넘겨주는 정보(데이터)의 가공
      (필터와 다르게 HttpServletRequest나 HttpServletResponse 등과 같은 객체를 제공받으므로 객체 자체를 조작할 수는 없음,
      대신 해당 객체가 내부적으로 갖는 값은 조작할 수 있으므로 컨트롤러로 넘겨주기 위한 정보를 가공 가능
      EX) JWT 토큰 정보를 파싱해서 컨트롤러에게 사용자의 정보를 제공하도록 가공)


<br/>

- ***Aop***
  - 주로 '로깅', '트랜잭션', '에러 처리'등 비즈니스단의 메서드에서 조금 더 세밀하게 조정하고 싶을 때 사용
  - 메소드 전후의 지점에 자유롭게 설정이 가능  
    (Interceptor나 Filter와는 달리)
  - AOP는 주소, 파라미터, 애노테이션 등 PointCut이 지원하는 다양한 방법으로 대상을 지정 가능
    (Interceptor와 Filter: 주소(URL)로 대상을 구분해서 걸러내야함)
  - URL 기반이 아닌 PointCut 단위로 동작
  - 비즈니스 로직의 메서드 실행 전, 후 단위까지 핸들링 가능

<br/>
<br/>

{: .prompt-tip }
> - Interceptor, Filter : Servlet 단위에서 실행됨
> - AOP : 메소드 앞에 Proxy패턴의 형태로 실행된다.

<br/>
<br/>

# Request가 들어올때 거치는 순서

---

요청이 들어오면  

Filter → Interceptor → AOP → Interceptor → Filter   

순으로 실행됩니다.  

<br/>

![스크린샷](https://user-images.githubusercontent.com/109974940/216751327-1817906e-383d-462a-8e2e-5b395509d265.png)

<br/>


1. 서버를 실행시켜 서블릿이 올라오는 동안에 init이 실행되고, 그 후 doFilter가 실행된다.

2. 컨트롤러에 들어가기 전 preHandler가 실행된다

3. 컨트롤러에서 나와 postHandler, after Completion, doFilter 순으로 진행이 된다.

4. 서블릿 종료 시 destroy가 실행된다.

<br/>
<br/>

---

(참고링크)

- [[Spring] Filter, Interceptor, AOP 차이 및 AOP를 사용하여 Logging을 구현한 이유](https://velog.io/@miot2j/Spring-Filter-Interceptor-AOP-%EC%B0%A8%EC%9D%B4-%EB%B0%8F-AOP%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EC%97%AC-Logging%EC%9D%84-%EA%B5%AC%ED%98%84%ED%95%9C-%EC%9D%B4%EC%9C%A0
  )
- [](https://goddaehee.tistory.com/154)

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>

<!--

❤️면접예상질문 ❤️

-->

