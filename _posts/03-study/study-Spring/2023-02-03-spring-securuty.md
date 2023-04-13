---
title: /Spring/ Spring Security, JWT
author: ggggraceful
date: 2023-02-03
categories: [03.STUDY, Spring]
tags: [study]
---

<br/>
<br/>

# Spring Security

---

- Spring 기반의 어플리케이션의 보안(인증과 권한, 인가 등)을 담당하는  
  스프링 하위 프레임워크
- '인증'과 '권한'에 대한 부분을 Filter 흐름에 따라 처리

<br/>
<br/>

# Spring Security의 구조

---

<br/>

- 세션-쿠키방식으로 인증

<br/>

{: .prompt-tip }
> 세션에 사용자 정보를 저장한다는 것  
> = 전통적인 세션-쿠키 기반의 인증 방식을 사용한다는 것을 의미

<br/>
<br/>

![스크린샷](https://user-images.githubusercontent.com/109974940/216748477-43fef865-d085-4b5e-927f-6e8ce2b8c1f6.png)

<br/>
<br/>

1.　유저가 로그인을 시도하면  
　　사용자가 입력한 정보를 가지고 인증을 요청한다. (```Request```)

---

2.　```AuthenticationFilter```는 이를 가로채    
　　```UsernamePasswordAuthenticationToken(인증용 객체)```를 생성한다.

---

3.　필터는  
　　요청을 처리하고  
　　```AuthenticationManager```의 구현체 ```ProviderManager```에   
　　Authentication과 UsernamePasswordAuthenticationToken을 전달한다.  

---

4.　AuthenticationManager는  
　　검증을 위해 ```AuthenticationProvider```에게  
　　Authentication과 UsernamePasswordAuthenticationToken을 전달한다.  

---

5.　DB에 담긴 사용자 인증정보와 비교하기 위해  
　　```UserDetailsService```에 사용자 정보를 넘겨준다.  

---

6.　user DB로 들어가   
　　존재하는 유저라면  
　　```UserDetails``` 로 객체를 만든다.

---

7.　```AuthenticationProvider```는  
　　UserDetails를 넘겨받고 비교한다.

---

8.　인증이 완료되면  
　　권한과 사용자 정보를 담은 ```Authentication정보```를 전달한다.   

---

9.　그 후 ```AuthenticationFilter```까지 Authentication 객체가 반환된다. 

---

10.　Authentication정보는  
　　SecurityContextHolder 세션 영역에 있는 ```SecurityContext```에  
　　UsernamePasswordAuthenticationToken(Authentication) 객체를 저장하고,  
　　➡️ 성공시 Authentication```Success```Handle를 실행
　　➡️ 실패시 Authentication```Failure```Handler 실행

<br/>
<br/>

# JWT

---

- JSON 포맷을 이용해 정보를 가볍고 안전하게 전송하기 위한  
  Claim 기반의 Web Token

- 일반적으로 클라이언트와 서버, 서비스와 서비스 사이 통신 시
  권한 인가(Authorization)을 위해 사용하는 토큰

- 사용자 로그인 시 서버는 사용자 인증을 완료하고  
  외부에 노출되어도 문제가 없는 인증관련 정보(사용자 ID, 권한 등)를 JSON 형태로 만든다.  
  이 데이터를 base64 인코딩을 해서 문자열을 만들고,  
  미리 정한 시스템의 SecretKey를 이용하여 서명 문자열을 생성한다.  

<br/>
<br/>

# JWT 구조

---

일반적으로 JWT의 구조는  
헤더, 페이로드, 서명 세 부분을 점으로 구분된다.  

<br/>

HEADER.PAYLOAD.SIGNATURE

- 헤더: 토큰 타입과 해싱 알고리즘
- 페이로드: 실제로 전달하는 정보
- 서명: 위변조를 방지하기 위한 값


![스크린샷](https://user-images.githubusercontent.com/109974940/216749952-4ebb3e8c-c0a8-4d62-b304-57645fadbba0.png)

<br/>
<br/>

# JWT 발급 과정

---

<br/>
<br/>

![스크린샷](https://user-images.githubusercontent.com/109974940/216749829-240b0500-84e7-45a7-8fa2-42fcbc3259a0.png)

<br/>

![스크린샷](https://user-images.githubusercontent.com/109974940/216749869-7161a2b5-32a0-49d4-8d09-ea983a6b1845.png)

<br/>
<br/>


1.　클라이언트에서  
　　로그인에 검증 가능한 ID, PW를 실어서 서버로 보낸다.  

---

2.　서버는 사용자 인증이 완료될 시  
　　JWT토큰을 생성해서 ```Body```에 담아 클라이언트에게 응답한다. 

--- 

3.　클라이언트는  
　　앞으로 로그인을 제외한 다른 api를 요청할 때마다   
　　```header```에 토큰을 실어서 보낸다. 

---

4.　서버에서는 다시 header에 실려온 토큰을 검증후 인증되면 응답을 해준다.  
　　(권한이 있는 사용자에게 리소스를 제공)

<br/>
<br/>

---

(참고링크)

- [[Spring] Spring Security와 JWT 개념](https://velog.io/@modsiw/Spring-Spring-Security%EC%99%80-JWT-%EA%B0%9C%EB%85%90)
- [(4) 로그인1 -SpringSecurity & JWT 개념](https://pozafly.github.io/tripllo/(4)spring-security-jwt/)
- [OpenAPI API 인증](https://scienceon.kisti.re.kr/apigateway/api/way/guide/tokenGuide.do;jsessionid=997B0FA3B10F439E122E67DEF3C56F42.apigateway_right)
- [[JWT] JSON Web Token 소개 및 구조](https://velopert.com/2389)

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>

<!--

❤️면접예상질문 ❤️

-->

