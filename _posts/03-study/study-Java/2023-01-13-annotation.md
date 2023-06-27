---
title: /Java/ Annotation
author: ggggraceful
date: 2023-01-13
categories: [03.STUDY, Java]
tags: [study, java]
---

<br/>
<br/>

## 📌 Annotation

---

- 사전적 의미로는 주석이라는 뜻이다.
- 클래스와 메서드에 추가하는 것이다.
- 특별한 의미를 부여하거나 다양한 기능을 부여하는 역할을 한다.
- 주로 데이터를 문서화하거나, 컴파일 타임이나 런타임시에 원하는 동작을 수행할 수 있도록 하는 데 사용된다.
- 프로그램에게 추가적인 정보를 제공해주는 메타데이터라고 볼 수 있다.  
  (meta data : 데이터를 위한 데이터)
- 어노테이션이 나오기 전까지 메타데이터는 프로퍼티 파일과 XML파일을 활용하였다.

<br/>
<br/>


### Annotation 장점

---

- 코드량 감소, 코드의 가독성 증대
 - 관련 코드 곁에 메타데이터를 설정할 수 있으므로 코드의 가독성 증대 됨
- 개발 효율성 증대
  - 복잡한 XML 스키마를 파악하지 않아도 됨
  - 개발시 개발 툴과 컴파일러의 도움을 받을 수 있으므로 개발 효율성이 증대됨
- 유지보수하기도 쉬워짐
- 생산성도 증가됨
- 별도의 파서를 적용하지 않고도 간단히 런타임 시에 활용할 수 있는 편리함
- JUnit, Framework, Permission Module 에서 사용


<br/>
<br/>

### Annotaion 단점

---

- 모듈 또는 애플리케이션의 메타 데이터를 설정할 수 없다.
- 클래스 단위 패키지 레벨이 한정되기 때문에  
  여러 클래스에 공통적으로 어노테이션을 설정할 수 없다. 
    <br/>
    <br/>

### Annotaion 사용순서

---

1. 어노테이션을 정의한다.
2. 클래스에 애노테이션을 배치한다.
3. 코드가 실행되는 중에 ```Reflection```을 이용하여 추가 정보를 획득하여 기능을 실시한다.

<br/>

{: .prompt-info }

✔️ Reflection  
 Reflection이란 프로그램이 실행 중에 자신의 구조와 동작을 검사하고, 조사하고, 수정하는 것이다.
Reflection은 프로그래머가 데이터를 보여주고, 다른 포맷의 데이터를 처리하고, 통신을 위해 serialization(직렬화)를 수행하고, bundling을 하기 위해 일반 소프트웨어 라이브러리를 만들도록 도와준다.Annotation 자체는 아무런 동작을 가지지 않는 단순한 표식일 뿐이지만, Reflection을 이용하면 Annotation의 적용 여부와 엘리먼트 값을 읽고 처리할 수 있다.

<br/>
<br/>

###  Anotation의 형태

---

1. Marker Annotation  
   - 이름만 있는 어노테이션
   - @AnnotationName

2. Single-Element Annotation
   - 하나의 원소만을 가지고 있는 어노테이션
   - @AnnotationName(elementValue)
   
3. Normal Annotation
   - 여러 개의 원소를 갖는 어노테이션
   - @AnnotationName(element=value, element=value, ...)

 <br/>
 <br/>

## 📌 Annotaion의 종류

---

<br/>

### 1. Spring의 대표적인 Annotaion의 종류

---

- @Component
  - 개발자가 생성한 Class를 Spring의 Bean으로 등록할 때 사용하는 Annotation입니다. 
  - Spring은 해당 Annotation을 보고 Spring의 Bean으로 등록합니다. 

<br/>

- @ComponentScan
  - Spring Framework는 @Component, @Service, @Repository, @Controller, @Configuration 중 1개라도 등록된 클래스를 찾으면, Context에 bean으로 등록합니다. 
  - @ComponentScan Annotation이 있는 클래스의 하위 Bean을 등록 될 클래스들을 스캔하여 Bean으로 등록해줍니다.

<br/>

- @Bean
  - @Bean Annotation은 개발자가 제어가 불가능한 외부 라이브러리와 같은 것들을 Bean으로 만들 때 사용합니다.

<br/>

- @Controller
  - Spring에게 해당 Class가 Controller의 역할을 한다고 명시하기 위해 사용하는 Annotation입니다.

<br/>

- @RequestHeader
  - Request의 header값을 가져올 수 있으며, 해당 Annotation을 쓴 메소드의 파라미터에 사용합니다.

<br/>

- @RequestMapping
  - @RequestMapping(value=”“)와 같은 형태로 작성
  - 요청 들어온 URI의 요청과 Annotation value 값이 일치하면 해당 클래스나 메소드가 실행됩니다. 
  - Controller 객체 안의 메서드와 클래스에 적용 가능
  - Class 단위에 사용하면 하위 메소드에 모두 적용됩니다.
  - 메소드에 적용되면 해당 메소드에서 지정한 방식으로 URI를 처리합니다.

<br/>

- @RequestParam
  - URL에 전달되는 파라미터를 메소드의 인자와 매칭시켜, 파라미터를 받아서 처리할 수 있는 Annotation으로 아래와 같이 사용합니다. 
  - Json 형식의 Body를 MessageConverter를 통해 Java 객체로 변환시킵니다.

<br/>

- @RequestBody
  - Body에 전달되는 데이터를 메소드의 인자와 매칭시켜, 데이터를 받아서 처리할 수 있는 Annotation으로 아래와 같이 사용합니다. 
  - 클라이언트가 보내는 HTTP 요청 본문(JSON 및 XML 등)을 Java 오브젝트로 변환합니다. 
  - 클라이언트가 body에 json or xml 과 같은 형태로 형태로 값(주로 객체)를 전송하면,  
    해당 내용을 Java Object로 변환합니다.

<br/>

- @ModelAttribute
  - 클라이언트가 전송하는 HTTP parameter, Body 내용을 Setter 함수를 통해 1:1로 객체에 데이터를 연결(바인딩)합니다. 
  - RequestBody와 다르게 HTTP Body 내용은 multipart/form-data 형태를 요구합니다. 
  - @RequestBody가 json을 받는 것과 달리 @ModenAttribute 의 경우에는 json을 받아 처리할 수 없습니다.

<br/>

- @ResponseBody
  - @ResponseBody은 메소드에서 리턴되는 값이 View 로 출력되지 않고 HTTP Response Body에 직접 쓰여지게 됩니다.
  - return 시에 json, xml과 같은 데이터를 return 합니다.

<br/>

- @Autowired
  - Spring Framework에서 Bean 객체를 주입받기 위한 방법은 크게 아래의 3가지가 있습니다. 
  - Bean을 주입받기 위하여 @Autowired 를 사용합니다. 
  - Spring Framework가 Class를 보고 Type에 맞게(Type을 먼저 확인 후, 없으면 Name 확인) Bean을 주입합니다.

    - @Autowired
    - 생성자 (@AllArgsConstructor 사용)
    - setter

<br/>

- @GetMapping
  - RequestMapping(Method=RequestMethod.GET)과 똑같은 역할을 함
  
<br/>

- @PostMapping
  - RequestMapping(Method=RequestMethod.POST)과 똑같은 역할함

<br/>

- @SpringBootTest
  - Spring Boot Test에 필요한 의존성을 제공해줍니다.

<br/>

- @Test
  - JUnit에서 테스트 할 대상을 표시합니다.

<br/>

- @configuration 
 - 외부라이브러리 또는 내장 클래스를 Bean으로 등록하고자 할 경우 사용(개발자가 직접 제어가 불가능한 클래스)
1개 이상의 @Bean을 제공하는 클래스의 경우 반드시 @Configuration을 사용. 
 - 해당 클래스에서 한 개 이상의 Bean을 생성하고 있을때 선언 해주어야 함

<br/>

- @Transaction
 - 데이터베이스의 상태를 변경하는 작업 또는 한번에 수행되어야 하는 연산들을 의미하고,
 - 예외 발생 시 rollback 처리를 자동으로 수행해주는 어노테이션입니다.
 - +추후 다른 글에서 자세하게 다룰 예정

  
<br/>
<br/>

### 2. Lombok의 대표적인 Annotation

---

:Lombok은 코드를 크게 줄여주어 가독성을 크게 높힐 수 있는 라이브러리

- @Setter
  - Class 모든 필드의 Setter method를 생성해줍니다.

<br/>

- @Getter
  - Class 모든 필드의 Getter method를 생성해줍니다.

<br/>

- @AllArgsConstructor
  - Class 모든 필드 값을 파라미터로 받는 생성자를 추가합니다.

<br/>

- @NoArgsConstructor
  - Class 기본 생성자를 자동으로 추가해줍니다.

<br/>

- @ToString
  - Class 모든 필드의 toString method를 생성한다.

<br/>
<br/>

---

## 📌 Annotation 비교

---

<br/>

###  @Component / @Configuration

---

@Componenet와 @Configuration은 큰 차이는 없다.  
하지만, @Configuration의 선언부를 보면 @Component가 정의되어 있으며,  
@Component는 개발자가 작성한 클래스를 Bean으로 등록하고자 할 때 사용한다.

<br/>

✔️ @Componenet

- 개발자가 직접 작성한 클래스를 Bean으로 등록하고자 할 경우 사용
- @Controller, @Service, @Repository 등의 어노테이션에서 상속

<br/>

✔️ @Configuration

- 외부라이브러리 또는 내장 클래스를 Bean으로 등록하고자 할 경우 사용(개발자가 직접 제어가 불가능한 클래스)
- 1개 이상의 @Bean을 제공하는 클래스의 경우 반드시 @Configuration을 사용.  
  즉, 해당 클래스에서 한 개 이상의 Bean을 생성하고 있을때 선언 해주어야 함

<br/>
- 개발자가 직접 제어 가능 : @Component
- 개발자가 직접 제어 불가능 : @Configuration, @Bean

<br/>
<br/>

---

(참고)
- [스프링(Spring)에서 자주 사용하는 Annotation 개념 및 예제 정리](https://melonicedlatte.com/2021/07/18/182600.html)
- [@ Annotation이란?](https://velog.io/@ruinak_4127/Annotation%EC%9D%B4%EB%9E%80)
- [[Spring] @Component와 @Configuration](https://velog.io/@albaneo0724/Spring-Component%EC%99%80-Configuration%EC%9D%98-%EC%B0%A8%EC%9D%B4)
- [Annotation](http://wiki.gurubee.net/display/DEVSTUDY/Annotation)
- [@Annotaion 의미와 종류](https://joohoon.tistory.com/31)

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>


<!--

❤️면접예상질문 ❤️

-->
