---
title: /Spring/ Transaction
author: ggggraceful
date: 2023-01-15
categories: [03.STUDY, Spring]
tags: [STUDY]
---

<br/>
<br/>

## 📌 트랜잭션

---

- Transactional이란 어노테이션은  
  데이터베이스의 ```상태를 변경```하는 작업 또는 한번에 수행되어야 하는 연산들을 의미
- 예외 발생 시 rollback 처리를 자동으로 수행해주는 어노테이션
- ACID라 하는 네가지 특성을 가지고 있습니다.

{: .prompt-info }
✔️상태를 변경시킨다는 것  
= SQL 질의어를 통해 DB에 접근하는 것  
-SELECT  
-INSERT  
-DELETE  
-UPDATE  

<br/>
<br/>

### 트랜잭션의 4가지 조건(ACID)

---

1. 원자성(Atomicity) 
   - 한 트랜잭션 내에서 실행한 작업들은 하나의 단위로 처리한다.  (모두 성공 또는 모두 실패)  
   - 트랜잭션이 DB에 모두 반영되거나, 혹은 전혀 반영되지 않아야 된다.

2. 일관성(Consistency)
   - 트랜잭션은 일관성 있는 데이터베이스 상태를 유지한다.  (data integrity 만족 등)
   - 트랜잭션의 작업 처리 결과는 항상 일관성 있어야 한다.

3. 격리성/독립성/고립성(Isolation)
   - 동시에 실행되는 트랜잭션들이 서로 영향을 미치지 않도록 격리해야 한다.
   - 둘 이상의 트랜잭션이 동시에 병행 실행되고 있을 때,   
     어떤 트랜잭션도 다른 트랜잭션 연산에 끼어들 수 없다.

4. 영속성/지속성(Durability)
   - 트랜잭션을 성공적으로 마치면 결과가 항상 저장되어야 한다.
   - 트랜잭션이 성공적으로 완료되었으면, 결과는 영구적으로 반영되어야 한다.

<br/>
<br/>

### 트랜잭션의 사용시 발생할 수 있는 문제점

---

- 현금 인출기를 작동하는 도중에 기계오류나 정전 등과 같은 예기치 않은 상황이 발생하여 카드가 나오지 않거나 기계
  가 멈추는 경우

- 각 각 다른 지점의 은행에서 동시에 인출할 때, 하나의 지점이 다른지점에서 저장한 잔액을 덮어 쓰는 경우

위와 같은 상황이 발생되지 않도록 방지하기 위해,  
즉 트랜잭션의 성질인 ACID 를 제공받기위해 트랜잭션을 사용한다

<br/>
<br/>

### 트랜잭션의 상태

---

- 활동 (Active)
    - 트랜잭션이 실행 중에 있는 상태, 연산들이 정상적으로 실행 중인 상태

- 장애 (Failed)
    - 트랜잭션이 실행에 오류가 발생하여 중단된 상태

- 철회 (Aborted)
    - 트랜잭션이 비정상적으로 종료되어 Rollback 연산을 수행한 상태

- 부분 완료 (Partially Committed)
    - 트랜잭션이 마지막 연산까지 실행했지만, Commit 연산이 실행되기 직전의 상태

- 완료 (Committed)
    - 트랜잭션이 성공적으로 종료되어 Commit 연산응 실행한 후의 상태

<br/>
<br/>

### 트랜잭션의 연산

---

하나의 트랜잭션은 commit 되거나, rollback 된다.

- Commit
    - 하나의 트랜잭션이 성공적으로 끝났고,   
      DB가 일관성있는 상태일 때 이를 알려주기 위해 사용하는 연산
    - 트랜잭션 안의 작업 내용 반영 (INSERT, UPDATE, DELETE ...)

- Rollback
    - 하나의 트랜잭션 처리가 비정상적으로 종료되어 트랜잭션 원자성이 깨진 경우  
      이 트랜잭션의 일부가 정상적으로 처리되었더라도  
      트랜잭션의 원자성을 구현하기 위해 이 트랜잭션이 행한 모든 연산을 취소(undo)하는 연산
    - transaction이 정상적으로 종료되지 않았을 때,  
      last consistent state(Transaction의 시작 상태 등)로 roll back 할 수 있음.
    - 트랜잭션 안의 작업 내용 반영안함 (INSERT, UPDATE, DELETE ...)

<br/>
<br/>

### 트랜잭션의 전파속성

---

Propagation(전파속성)

Spring이 제공하는 선언적 트랜잭션(트랜잭션 어노테이션, @Transactional)의 장점 중 하나는 여러 트랜잭션을 묶어서 커다란 하나의 트랜잭션 경계를 만들 수 있다는 점이다. 작업을 하다보면 기존에 트랜잭션이 진행중일 때 추가적인 트랜잭션을 진행해야 하는 경우가 있다.   
 
- 이미 트랜잭션이 진행중일 때 추가 트랜잭션 진행을 어떻게 할지 결정하는 것이 전파 속성(Propagation)이다.  

전파 속성에 따라 기존의 트랜잭션에 참여할 수도 있고,  
별도의 트랜잭션으로 진행할 수도 있고,  
에러를 발생시키는 등 여러 선택을 할 수 있다.  

이렇게 하나의 트랜잭션이 다른 트랜잭션을 만나는 상황을 그림으로 나타내면 다음과 같다.

![사진](https://user-images.githubusercontent.com/109974940/213606987-037be3a1-b2ba-4002-a0a8-fe7f3d93e9e9.png)


<br/>
<br/>

### 트랜잭션의 격리수준

---

Isolation(격리수준, 고립레벨)

트랜잭션 격리가 성공하는 정도의 측정값을 말한다.  
(SQL 의 Isolation level 과 동일하게 동작)

- [Level 0] Read Uncommitted
  - commit 되지 않은 데이터를 읽는다.
  - select 수행하는 동안 해당 데이터에 Shared lock이 걸리지 않는다.

- [Level 1] Read Committed
  - commit 된 데이터만 읽는다.
  - select 수행하는 동안 해당 데이터에 Shared lock이 걸린다. 

- [Level 2] Repeatable Read
  - 자신의 트랜잭션이 생성되기 이전의 트랜잭션(낮은 번호의 트랜잭션)의 커밋된 데이터만 읽는다.
  - 트랜잭션이 완료될 때까지 해당 데이터 수정이 불가능하다.

- [Level 3] Serializable
  - LOCK 을 걸고 사용
  - 트랜잭션이 완료될 때까지 해당 데이터 수정, 입력이 불가능하다.

- DEFAULT : 사용하는 DB 기본 설정을 따른다. (Oracle 은 READ_COMMITED, Mysql InnoDB 는 REPEATABLE_READ 가 Default)

<br/>
<br/>

---

(참고)

- [DB 트랜잭션(Transaction)](https://kafcamus.tistory.com/30)
- [](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/Transaction.md)
- [DBMS는 어떻게 트랜잭션을 관리할까?](https://d2.naver.com/helloworld/407507)
- [03. 기술 면접 - 데이터베이스 - 트랜잭션](https://theheydaze.tistory.com/582)
- [[Spring] 스프링의 트랜잭션 전파 속성(Transaction propagation) 완벽하게 이해하기](https://mangkyu.tistory.com/269)
- [트랜잭션 전파 속성 ( propagation ), 롤백 예외](https://happyer16.tistory.com/entry/%ED%8A%B8%EB%9E%9C%EC%9E%AD%EC%85%98-%EC%A0%84%ED%8C%8C-%EC%86%8D%EC%84%B1-propagation-%EB%A1%A4%EB%B0%B1-%EC%98%88%EC%99%B8)
- [back/Spring Framework @Transactional Propagation (전파속성), Isolation (격리수준레벨) 그리고 synchronized](https://developyo.tistory.com/250)
- [[Spring/DB] @Transactional의 전파 속성과 고립 레벨](https://velog.io/@ej_shin/SpringDB-Transactional%EC%9D%98-%EC%A0%84%ED%8C%8C-%EC%86%8D%EC%84%B1%EA%B3%BC-%EA%B3%A0%EB%A6%BD-%EB%A0%88%EB%B2%A8)
- [Transaction 전파가 뭡니까?](https://velog.io/@myspy/Transaction-%EC%A0%84%ED%8C%8C%EA%B0%80-%EB%AD%A1%EB%8B%88%EA%B9%8C)

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다. 참고는 맨 아래 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>

<!--

❤️면접예상질문 ❤️

-->
