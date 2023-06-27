---
title: /JPA/ 즉시로딩, 지연로딩
author: ggggraceful
date: 2023-01-23
categories: [03.STUDY, JPA]
tags: [study, jpa]
---

<br/>
<br/>

{: .prompt-tip }
> fetch의 디폴트 값
> -@xxToOne: EAGER
> -@xxToMany: LAZY

<br/>

# 1. 즉시로딩

---

EAGER LOADING

```java
@xxToxx(fetch = fetchType.EAGER)
```

- 엔티티를 조회할 때 연관된 엔티티도 함께 조회  
  (= 연관된 엔티티를 즉시조회)
- 하이버네이트는 가능하면 SQL조인을 사용해서 한번에 조회
  (JPA 구현체는 즉시 로딩을 최적화하기 위해 가능하면 조인쿼리를 사용)

<br/>

- 장점
  - 지연된 초기화와 관련해서 성능적인 영향이 없음
  - 즉시 로딩(Earge Loading) 

<br/>

- 단점
  - 지연 로딩보다 긴 초기의 로딩 시간이 필요함
  - 불필요한 데이터를 많이 로딩하면 성능에 영향을 줄 수 있음

<br/>

{: .prompt-info }
> ✔️하이버네이트
> -자바 언어를 위한 ORM 프레임워크이고 JPA의 구현체로,  
> 　 JPA 인터페이스를 구현하고 내부적으로 JDBC API를 사용한다.
> -자바객체를 통해 데이터베이스가 Oracle, MySql, MSSQL 등에 상관없이  
> 　 다룰수 있도록 하는 추상화를 목표로 한다.

<br/>
<br/>

# 2. 지연로딩 

---

LAZY LOADING

```java
@xxToxx(fetch = fetchType.LAZY)
```
- 엔티티를 조회할 때 연관된 엔티티는 프록시로 조회되며,  
  프록시를 실제 사용할 때 초기화되면서 데이터베이스를 조회
- 가급적이면 기본적으로 지연 로딩을 사용하는 것이 좋다.

<br/>

- 장점
  - 다른 접근 방식보다 훨씬 적은 초기의 로딩 시간
  - 다른 접근 방식에 비해 메모리 소비량 감소
  - 지연 로딩(Lazy Loading) 

<br/>

- 단점
  - 초기화가 지연되면 원하지 않는 순간 성능에 영향을 줄 수 있음

<br/>

{: .prompt-info }
> ✔️ 프록시
> -클라이언트가 이를 통해서 통해서 다른 네트워크 서비스에 간접적으로 접속할 수 있게 해 주는 컴퓨터 시스템이나 응용 프로그램
> -서버와 클라이언트 사이에 중계기로서 대리로 통신을 수행하는 것을 가리켜 '프록시',  
>   그 중계 기능을 하는 것을 프록시 서버라고 부른다.

<br/>
<br/>

# 3. 언제 사용하면 좋은가

---

- 즉시로딩
  - 쿼리문을 두 번 따로 사용하여 조회하지 않고  
    연관된 엔티티를 즉시 조회하는 게 더 유리할 때 사용하면 좋다.

<br/>

- 지연 로딩
  - 필요한 시점에 연관된 엔티티를 조회하여 로딩 시간을 줄이고,  
    불필요한 쿼리문 사용을 방지할 수 있어  
    가급적이면 기본적으로 지연 로딩을 사용하는 것이 좋다.
  
<br/>
<br/>

# 4. 주의할 점

---

- 즉시로딩을 적용하면 예상하지 못한 SQL이 발생할 수 있음
- 즉시로딩은 JPQL에서 N+1 문제를 일으킴
- 즉시로딩의 큰 문제는 성능 최적화가 어렵다는 점

<br/>

➡️ 가급적이면 지연 로딩(Lazy Loading)만 사용하고,  
　　 성능 최적화가 꼭 필요한 곳에는 JPQL 페치 조인을 사용하는 것이 좋다. 

기본값이 즉시로딩음 @--ToOne을 fetch = FetchType.LAZY로 설정해  
지연 로딩 전략을 사용하도록 변경하는 것이 좋다. 


<br/>
<br/>

---

(참고)

- [[JPA] 즉시 로딩과 지연 로딩(FetchType.LAZY or EAGER)](https://ict-nroo.tistory.com/132)
- [JPA 지연로딩을 사용해야하는 이유, 지연로딩(Lazy)과 즉시로딩(Eager)](https://developer-hm.tistory.com/37)
- [하이버네이트(Hidernate) 설명 및 설정법](https://devbksheen.tistory.com/entry/JPA-%ED%95%98%EC%9D%B4%EB%B2%84%EB%84%A4%EC%9D%B4%ED%8A%B8)
- [Spring Data JPA 즉시 로딩(Eager Loading) & 지연 로딩(Lazy Loading)](https://zzang9ha.tistory.com/347)

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>

<!--

❤️면접예상질문 ❤️

+ 프록시

-->
