---
title: /Spring/ Spring bean container
author: ggggraceful
date: 2023-02-04
categories: [03.STUDY, Spring]
tags: [study, spring]
---

<br/>
<br/>

# Spring bean container

---

- 자바 객체의 생명 주기를 관리하며, 생성된 자바 객체들에게 추가적인 기능을 제공하는 역할  
  여기서 말하는 자바 객체를 스프링에서는 빈(Bean)이라고 부른다.
- IoC와 DI의 원리가 이 스프링 컨테이너에 적용됨
- 개발자는 new 연산자, 인터페이스 호출, 팩토리 호출 방식으로 객체를 생성하고 소멸시킬 수 있는데,  
  스프링 컨테이너가 이 역할을 대신해 준다.(=제어 흐름을 외부에서 관리)
- 객체들 간의 의존 관계를 스프링 컨테이너가 런타임 과정에서 알아서 만들어 준다.  
  (생성자, setter, @Autowired를 통해 적용)

<br/>

- 장점
  - 스프링 종속적인 기술이 아니라 자바 표준이기에  
    다른 컨테이너에서도 동작하고, 컴포넌트 스캔과 잘 어울린다.  

- 단점
  - 외부 라이브러리에는 적용하지 못한다. 


<br/>
<br/>

# Spring bean container 생성부터 스프링 종료까지의 사이클

---

스프링 IoC 컨테이너가 생성되면  
Component-Scan으로 Bean을 등록하고,  
IoC컨테이너에서 의존성을 주입한다.  

스프링은 Bean에게  
콜백 메서드를 통해 초기화 시점을 알려주며,    

스프링 컨테이너가 종료되기 직전에도  
소멸 콜백 메서드를 통해  
소멸 시점을 알려주고 스프링이 종료된다.

<br/>
<br/>

# @PostConstruct, @PreDestroy 어노테이션의 역할

---

최근 스프링에서 빈 생명주기 콜백을 관리하는 방법 중 가장 권장하는 방법이  
@PostConstruct, @PreDestroy 어노테이션을 이용하는 방법입니다.

- ***@PostConstruct***
  - 초기화 콜백을 동작시킬 수 있음
  - 의존관계 주입이 완료되면 호출됨

- ***@PreDestroy***
  - 소멸 콜백을 동작시킬 수 있음
  - 빈이 소멸되기 직전에 호출됨

<br/>
<br/>







<br/>
<br/>

---

(참고링크)

- [[Spring] 스프링 컨테이너와 빈이란?](https://steady-coding.tistory.com/459)

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>

<!--

❤️면접예상질문 ❤️

-->

