---
title: /Spring/ Transaction
author: ggggraceful
date: 2023-01-15
categories: [03.STUDY, Spring]
tags: [STUDY]
---

<br/>
<br/>

## π νΈλμ­μ

---

- Transactionalμ΄λ μ΄λΈνμ΄μμ  
  λ°μ΄ν°λ² μ΄μ€μ ```μνλ₯Ό λ³κ²½```νλ μμ λλ νλ²μ μνλμ΄μΌ νλ μ°μ°λ€μ μλ―Έ
- μμΈ λ°μ μ rollback μ²λ¦¬λ₯Ό μλμΌλ‘ μνν΄μ£Όλ μ΄λΈνμ΄μ
- ACIDλΌ νλ λ€κ°μ§ νΉμ±μ κ°μ§κ³  μμ΅λλ€.

{: .prompt-info }
βοΈμνλ₯Ό λ³κ²½μν¨λ€λ κ²  
= SQL μ§μμ΄λ₯Ό ν΅ν΄ DBμ μ κ·Όνλ κ²  
-SELECT  
-INSERT  
-DELETE  
-UPDATE  

<br/>
<br/>

### νΈλμ­μμ 4κ°μ§ μ‘°κ±΄(ACID)

---

1. μμμ±(Atomicity) 
   - ν νΈλμ­μ λ΄μμ μ€νν μμλ€μ νλμ λ¨μλ‘ μ²λ¦¬νλ€.  (λͺ¨λ μ±κ³΅ λλ λͺ¨λ μ€ν¨)  
   - νΈλμ­μμ΄ DBμ λͺ¨λ λ°μλκ±°λ, νΉμ μ ν λ°μλμ§ μμμΌ λλ€.

2. μΌκ΄μ±(Consistency)
   - νΈλμ­μμ μΌκ΄μ± μλ λ°μ΄ν°λ² μ΄μ€ μνλ₯Ό μ μ§νλ€.  (data integrity λ§μ‘± λ±)
   - νΈλμ­μμ μμ μ²λ¦¬ κ²°κ³Όλ ν­μ μΌκ΄μ± μμ΄μΌ νλ€.

3. κ²©λ¦¬μ±/λλ¦½μ±/κ³ λ¦½μ±(Isolation)
   - λμμ μ€νλλ νΈλμ­μλ€μ΄ μλ‘ μν₯μ λ―ΈμΉμ§ μλλ‘ κ²©λ¦¬ν΄μΌ νλ€.
   - λ μ΄μμ νΈλμ­μμ΄ λμμ λ³ν μ€νλκ³  μμ λ,   
     μ΄λ€ νΈλμ­μλ λ€λ₯Έ νΈλμ­μ μ°μ°μ λΌμ΄λ€ μ μλ€.

4. μμμ±/μ§μμ±(Durability)
   - νΈλμ­μμ μ±κ³΅μ μΌλ‘ λ§μΉλ©΄ κ²°κ³Όκ° ν­μ μ μ₯λμ΄μΌ νλ€.
   - νΈλμ­μμ΄ μ±κ³΅μ μΌλ‘ μλ£λμμΌλ©΄, κ²°κ³Όλ μκ΅¬μ μΌλ‘ λ°μλμ΄μΌ νλ€.

<br/>
<br/>

### νΈλμ­μμ μ¬μ©μ λ°μν  μ μλ λ¬Έμ μ 

---

- νκΈ μΈμΆκΈ°λ₯Ό μλνλ λμ€μ κΈ°κ³μ€λ₯λ μ μ  λ±κ³Ό κ°μ μκΈ°μΉ μμ μν©μ΄ λ°μνμ¬ μΉ΄λκ° λμ€μ§ μκ±°λ κΈ°κ³
  κ° λ©μΆλ κ²½μ°

- κ° κ° λ€λ₯Έ μ§μ μ μνμμ λμμ μΈμΆν  λ, νλμ μ§μ μ΄ λ€λ₯Έμ§μ μμ μ μ₯ν μμ‘μ λ?μ΄ μ°λ κ²½μ°

μμ κ°μ μν©μ΄ λ°μλμ§ μλλ‘ λ°©μ§νκΈ° μν΄,  
μ¦ νΈλμ­μμ μ±μ§μΈ ACID λ₯Ό μ κ³΅λ°κΈ°μν΄ νΈλμ­μμ μ¬μ©νλ€

<br/>
<br/>

### νΈλμ­μμ μν

---

- νλ (Active)
    - νΈλμ­μμ΄ μ€ν μ€μ μλ μν, μ°μ°λ€μ΄ μ μμ μΌλ‘ μ€ν μ€μΈ μν

- μ₯μ  (Failed)
    - νΈλμ­μμ΄ μ€νμ μ€λ₯κ° λ°μνμ¬ μ€λ¨λ μν

- μ² ν (Aborted)
    - νΈλμ­μμ΄ λΉμ μμ μΌλ‘ μ’λ£λμ΄ Rollback μ°μ°μ μνν μν

- λΆλΆ μλ£ (Partially Committed)
    - νΈλμ­μμ΄ λ§μ§λ§ μ°μ°κΉμ§ μ€ννμ§λ§, Commit μ°μ°μ΄ μ€νλκΈ° μ§μ μ μν

- μλ£ (Committed)
    - νΈλμ­μμ΄ μ±κ³΅μ μΌλ‘ μ’λ£λμ΄ Commit μ°μ°μ μ€νν νμ μν

<br/>
<br/>

### νΈλμ­μμ μ°μ°

---

νλμ νΈλμ­μμ commit λκ±°λ, rollback λλ€.

- Commit
    - νλμ νΈλμ­μμ΄ μ±κ³΅μ μΌλ‘ λλ¬κ³ ,   
      DBκ° μΌκ΄μ±μλ μνμΌ λ μ΄λ₯Ό μλ €μ£ΌκΈ° μν΄ μ¬μ©νλ μ°μ°
    - νΈλμ­μ μμ μμ λ΄μ© λ°μ (INSERT, UPDATE, DELETE ...)

- Rollback
    - νλμ νΈλμ­μ μ²λ¦¬κ° λΉμ μμ μΌλ‘ μ’λ£λμ΄ νΈλμ­μ μμμ±μ΄ κΉ¨μ§ κ²½μ°  
      μ΄ νΈλμ­μμ μΌλΆκ° μ μμ μΌλ‘ μ²λ¦¬λμλλΌλ  
      νΈλμ­μμ μμμ±μ κ΅¬ννκΈ° μν΄ μ΄ νΈλμ­μμ΄ νν λͺ¨λ  μ°μ°μ μ·¨μ(undo)νλ μ°μ°
    - transactionμ΄ μ μμ μΌλ‘ μ’λ£λμ§ μμμ λ,  
      last consistent state(Transactionμ μμ μν λ±)λ‘ roll back ν  μ μμ.
    - νΈλμ­μ μμ μμ λ΄μ© λ°μμν¨ (INSERT, UPDATE, DELETE ...)

<br/>
<br/>

### νΈλμ­μμ μ νμμ±

---

Propagation(μ νμμ±)

Springμ΄ μ κ³΅νλ μ μΈμ  νΈλμ­μ(νΈλμ­μ μ΄λΈνμ΄μ, @Transactional)μ μ₯μ  μ€ νλλ μ¬λ¬ νΈλμ­μμ λ¬Άμ΄μ μ»€λ€λ νλμ νΈλμ­μ κ²½κ³λ₯Ό λ§λ€ μ μλ€λ μ μ΄λ€. μμμ νλ€λ³΄λ©΄ κΈ°μ‘΄μ νΈλμ­μμ΄ μ§νμ€μΌ λ μΆκ°μ μΈ νΈλμ­μμ μ§νν΄μΌ νλ κ²½μ°κ° μλ€.   
 
- μ΄λ―Έ νΈλμ­μμ΄ μ§νμ€μΌ λ μΆκ° νΈλμ­μ μ§νμ μ΄λ»κ² ν μ§ κ²°μ νλ κ²μ΄ μ ν μμ±(Propagation)μ΄λ€.  

μ ν μμ±μ λ°λΌ κΈ°μ‘΄μ νΈλμ­μμ μ°Έμ¬ν  μλ μκ³ ,  
λ³λμ νΈλμ­μμΌλ‘ μ§νν  μλ μκ³ ,  
μλ¬λ₯Ό λ°μμν€λ λ± μ¬λ¬ μ νμ ν  μ μλ€.  

μ΄λ κ² νλμ νΈλμ­μμ΄ λ€λ₯Έ νΈλμ­μμ λ§λλ μν©μ κ·Έλ¦ΌμΌλ‘ λνλ΄λ©΄ λ€μκ³Ό κ°λ€.

![μ¬μ§](https://user-images.githubusercontent.com/109974940/213606987-037be3a1-b2ba-4002-a0a8-fe7f3d93e9e9.png)


<br/>
<br/>

### νΈλμ­μμ κ²©λ¦¬μμ€

---

Isolation(κ²©λ¦¬μμ€, κ³ λ¦½λ λ²¨)

νΈλμ­μ κ²©λ¦¬κ° μ±κ³΅νλ μ λμ μΈ‘μ κ°μ λ§νλ€.  
(SQL μ Isolation level κ³Ό λμΌνκ² λμ)

- [Level 0] Read Uncommitted
  - commit λμ§ μμ λ°μ΄ν°λ₯Ό μ½λλ€.
  - select μννλ λμ ν΄λΉ λ°μ΄ν°μ Shared lockμ΄ κ±Έλ¦¬μ§ μλλ€.

- [Level 1] Read Committed
  - commit λ λ°μ΄ν°λ§ μ½λλ€.
  - select μννλ λμ ν΄λΉ λ°μ΄ν°μ Shared lockμ΄ κ±Έλ¦°λ€. 

- [Level 2] Repeatable Read
  - μμ μ νΈλμ­μμ΄ μμ±λκΈ° μ΄μ μ νΈλμ­μ(λ?μ λ²νΈμ νΈλμ­μ)μ μ»€λ°λ λ°μ΄ν°λ§ μ½λλ€.
  - νΈλμ­μμ΄ μλ£λ  λκΉμ§ ν΄λΉ λ°μ΄ν° μμ μ΄ λΆκ°λ₯νλ€.

- [Level 3] Serializable
  - LOCK μ κ±Έκ³  μ¬μ©
  - νΈλμ­μμ΄ μλ£λ  λκΉμ§ ν΄λΉ λ°μ΄ν° μμ , μλ ₯μ΄ λΆκ°λ₯νλ€.

- DEFAULT : μ¬μ©νλ DB κΈ°λ³Έ μ€μ μ λ°λ₯Έλ€. (Oracle μ READ_COMMITED, Mysql InnoDB λ REPEATABLE_READ κ° Default)

<br/>
<br/>

---

(μ°Έκ³ )

- [DB νΈλμ­μ(Transaction)](https://kafcamus.tistory.com/30)
- [](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Database/Transaction.md)
- [DBMSλ μ΄λ»κ² νΈλμ­μμ κ΄λ¦¬ν κΉ?](https://d2.naver.com/helloworld/407507)
- [03. κΈ°μ  λ©΄μ  - λ°μ΄ν°λ² μ΄μ€ - νΈλμ­μ](https://theheydaze.tistory.com/582)
- [[Spring] μ€νλ§μ νΈλμ­μ μ ν μμ±(Transaction propagation) μλ²½νκ² μ΄ν΄νκΈ°](https://mangkyu.tistory.com/269)
- [νΈλμ­μ μ ν μμ± ( propagation ), λ‘€λ°± μμΈ](https://happyer16.tistory.com/entry/%ED%8A%B8%EB%9E%9C%EC%9E%AD%EC%85%98-%EC%A0%84%ED%8C%8C-%EC%86%8D%EC%84%B1-propagation-%EB%A1%A4%EB%B0%B1-%EC%98%88%EC%99%B8)
- [back/Spring Framework @Transactional Propagation (μ νμμ±), Isolation (κ²©λ¦¬μμ€λ λ²¨) κ·Έλ¦¬κ³  synchronized](https://developyo.tistory.com/250)
- [[Spring/DB] @Transactionalμ μ ν μμ±κ³Ό κ³ λ¦½ λ λ²¨](https://velog.io/@ej_shin/SpringDB-Transactional%EC%9D%98-%EC%A0%84%ED%8C%8C-%EC%86%8D%EC%84%B1%EA%B3%BC-%EA%B3%A0%EB%A6%BD-%EB%A0%88%EB%B2%A8)
- [Transaction μ νκ° λ­‘λκΉ?](https://velog.io/@myspy/Transaction-%EC%A0%84%ED%8C%8C%EA%B0%80-%EB%AD%A1%EB%8B%88%EA%B9%8C)

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> κ³΅λΆν λ΄μ©μ μ¬λ¬κΈκ³Ό μ± μ½μ λ΄μ©μ λ°νμΌλ‘ μ λ¦¬νκ³  μμ΅λλ€. μ°Έκ³ λ λ§¨ μλ μμ΅λλ€.</span>  
<span style="font-size: 12px; color:  #cbce91"> μ’μ κΈλ‘ μ μ κ³΅λΆμ λμμ μ£Όμλ λΆλ€κ» κ°μ¬λλ¦½λλ€. </span>

<!--

β€οΈλ©΄μ μμμ§λ¬Έ β€οΈ

-->
