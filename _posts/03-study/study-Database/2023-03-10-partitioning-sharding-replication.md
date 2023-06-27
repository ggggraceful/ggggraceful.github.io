---
title: /Database/ 💬 파티셔닝, 샤딩, 리플리케이션
author: ggggraceful
date: 2023-03-10
categories: [03.STUDY, Database]
tags: [study, database]
---


<br/>
<br/>

# 파티셔닝 (partitioning)

---

database table을 더 작은 table들로 나누는 것

## vertical partitioning
- column을 기준으로 table을 나누는 방식

- 정규화도 이에 해당됨
  - 이미 정규화 되어있는 테이블이라고 퍼포먼스를 위해 버티컬 파티셔닝이 가능
  - (ex)  
    게시글 목록에는 게시글 내용이 보이지 않는데  
    데이터 용량이 큰 게시글 내용까지 한 테이블에 담게 되면   
    사용하지 않는 메모리까지도 선택되어 I/O에 부담을 주게됨.
    버티컬 파티셔닝을 해 테이블을 분리해서 사용하는 것이 좋음
  
- 민감한 정보에 접근 제한을 두기 위해 사용되기도 함
    
 
## horizontal partitioning
- row를 기준으로 table을 나누는 방

<br/>
<br/>

# 샤딩 (sharding)

---


<br/>
<br/>

# 리플리케이션 (replication)

---



<br/>
<br/>

---

(참고)

- [[DB] 파티셔닝? 샤딩? 레플리케이션? (partitioning? sharding? replication?)](https://www.youtube.com/watch?v=P7LqaEO-nGU)

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>

<!--

❤️면접예상질문 ❤️

-->
