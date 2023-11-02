---
title: /Database/ MAX+1과 시퀀스(Sequence) NEXTVAL 
author: ggggraceful
date: 2023-06-28
categories: [03.STUDY, Database]
tags: [study, database]
---

<br/>
<br/>

# DB에서 PK로 인덱스 번호를 1씩 증가하며 생성하는 방법

---

<br/>

- 시퀀스를 생성하여 NEXTVAL 함수로 증가시키는 방법
- 현재 시퀀스번호의 MAX값의 +1을 하는 사용방법

<br/>
<br/>

# 시퀀스

---

<br/>

- NEXTVAL : 다음번호 조회
- CURRVAL : 현재번호 조회

<br/>

```java
SELECT NVL(MAX(SEQ)+1, 1) FROM TABLE;
```

<br/>
<br/>

### 시퀀스의 단점

- 시퀀스는 생성하고 필요시 수정하고 관리를 해야되는 불편함

<br/>

### 시퀀스의 장점

- MAX+1로 조회해서 사용하는 경우 동시성이슈가 발생할 때 중복이 될 수 있기때문에
  시퀀스를 권장

<br/>
<br/>
<br/>

여러명의 사용자가 동시에 같은 번호의 PRIMARY KEY를 조회하게 되면
한명을 제외하고 EXCEPTION 처리가 됨.

<br/>

만약 PRIMARY KEY로 설정되지 않은 컬럼이라면
모두 다 똑같은 시퀀스번호가 생성되게 된다.

<br/>
<br/>

MAX + 1을 사용했다면
동시에 입력을 하는 상황이 왔다면
1,1,2,3,4,5,5,6,7,8 이런식으로 중복되는 PK가 생길 수 있다.

<br/>
<br/>

이런 동시성이슈가 발생할 때 중복이 될 수 있기 때문에
이를 방지하기 위해 Sequence.NEXTVAL 를 사용할 수 있다.

<br/>

Sequence.NEXTVAL 같은 경우에는
동시에 입력하는 경우
1,2,3,4,5,6,7,8,9,10 처럼
중복된 PK가 생기는 것을 방지할 수 있다.

<br/>
<br/>
<br/>

{: .prompt-info }
> Max+1 :  중복 사용 가능
> Sequence : 중복 사용 불가


<br/>
<br/>

---

(참고)

- (https://jfbta.tistory.com/99)[[시퀀스(Sequence) NEXTVAL 과 MAX+1의 사용방법 및 차이](https://jfbta.tistory.com/99)]
- (https://mine-it-record.tistory.com/63)[시퀀스(Sequence) 와 MAX +1 의 차이]







<br/>
<br/>

---

(참고)

- [..](..)

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>

<!--

❤️면접예상질문 ❤️

-->

