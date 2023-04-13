---
title: /JPA/ JPA의 더티체킹
author: ggggraceful
date: 2023-01-15
categories: [03.STUDY, JPA]
tags: [study]
---

<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다. 참고는 맨 아래 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>

<br/>
<br/>

JPA(Java Persistence API)를 사용하면서 더티 체킹과 트랜잭션의 관계에 대해서 알고 있지 않으면,
비즈니스 로직에서 다루는 엔티티 데이터가 꼬이는 경우가 발생할 수 있다.

데이터가 꼬이는 경우를 방지하려면,
더티 체킹(Dirty Checking)이 어떤 상황에 사용이 되는지 알고 있어야 한다.

## JPA 더티체킹

---

dirty checking

- JPA에서 엔티티 매니저는 엔티티를 저장/조회/수정/삭제를 하는데,  
  수정에 해당하는 메서드가 없고, 대신해서 더티체킹을 지원한다.  
- 더티 체킹이란 “상태 변경 검사” 또는 "변경감지"라고 한다.  
- Transaction 안에서 엔티티의 변경이 일어나면,  
  변경 내용을 자동으로 데이터베이스에 반영하는 JPA 특징이다.  
  (변경은 최초 조회 상태가 기준이다)

{: .prompt-info }
> *Dirty: 엔티티 데이터의 변경된 부분  
> *Dirty Checking : 변경된 부분을 체크해서 DB에 반영한다.

{: .prompt-info }
> ✔️ 데이터베이스에 변경 데이터를 저장하는 시점  
> -Transaction commit 시점  
> -EntityManager flush 시점  
> -JPQL 사용 시점  

<br/>
<br/>

### 더티체킹이 일어나는 환경

---

- 영속 상태(Managed) 안에 있는 엔티티인 경우
- Transaction 안에서 엔티티를 변경하는 경우

<br/>
<br/>

### 더티체킹의 과정

---

1. 트랜잭션을 커밋하면 엔티티 매니저 내부에서 먼저 플러시(flush())가 호출된다.
2. 엔티티와 스냅샷을 비교해서 변경된 엔티티를 찾는다.
3. 변경된 엔티티가 있으면 수정쿼리를 생성해서 쓰기 지연 SQL 저장소에 보낸다.
4. 쓰기 지연 저장소의 SQL을 데이터베이스에 보낸다.
5. 데이터베이스 트랜잭션을 커밋한다. 
6. update 쿼리는 없지만, save() 메서드로 저장하지 않아도 더티체킹으로 update 쿼리가 실행되어 update 쿼리가 데이터베이스로 전달된다. 

<br/>
<br/>

### 더티체킹의 특징

---

- 더티체킹의 대상  
: ```영속성 컨택스트(Persistence Context)``` 안에 있는 엔티티를 대상으로 더티 체킹이 일어난다.  
  (비영속, 준영속처럼 영속성 컨텍스트의 관리를 받지 못하는 엔티티는 값을 변경해도 데이터베이스에 반영되지 않는다.)

{: .prompt-info }
> ✔️ 영속성 콘텍스트  
> 영속성 컨텐스트란 엔티티를 영구 저장하는 환경이라는 뜻이다. 애플리케이션과 데이터베이스 사이에서 객체를 보관하는 가상의 데이터베이스 같은 역할을 한다. 엔티티 매니저를 통해 엔티티를 저장하거나 조회하면 엔티티 매니저는 영속성 컨텍스트에 엔티티를 보관하고 관리한다.

- 기본적으로 더티 체킹을 실행하면, SQL에서는 변경된 엔티티의 모든 내용을 update 쿼리로 만들어 전달하는데, 
  이때 필드가 많아지면 전체 필드를 update하는게 비효율적일 수도 있다.  
  이때는 @DynamicUpdate를 해당 Entity에 선언하여 변경 필드만 반영시키도록 만들어줄 수 있다

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다. 참고는 맨 아래 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>

---

(참고)

- [JPA 더티 체킹(Dirty Checking)이란?](https://interconnection.tistory.com/121)
- [[Spring JPA] Dirty Checking(더티체킹)이란?](https://frogand.tistory.com/175)
- [JPA 영속성 컨텍스트란?](https://velog.io/@neptunes032/JPA-%EC%98%81%EC%86%8D%EC%84%B1-%EC%BB%A8%ED%85%8D%EC%8A%A4%ED%8A%B8%EB%9E%80)
- [[Spring Data JPA] 더티 체킹 (Dirty Checking)](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Web/Spring/%5BSpring%20Data%20JPA%5D%20%EB%8D%94%ED%8B%B0%20%EC%B2%B4%ED%82%B9%20(Dirty%20Checking).md)


<!--

❤️면접예상질문 ❤️

-->
