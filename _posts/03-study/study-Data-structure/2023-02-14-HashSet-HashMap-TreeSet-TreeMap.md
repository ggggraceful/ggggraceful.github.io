---
title: /Data structure/ 💚 HashSet, HashMap, TreeSet, TreeMap
author: ggggraceful
date: 2023-02-14
categories: [03.STUDY, Data structure]
tags: [STUDY]
---

<br/>
<br/>

# Set, Map / Hash, Tree

---

<br/>

|          | set | Map |
|----------|-----|-----|
| 자료형태     |  Value 만 존재   |  Key, Value 쌍으로 존재   |
| 중복여부     |  중복 불가  |  Key값 중복 불가   |
| contains |  contains(value)   |  containsKey(key)   |
| get      |  불가   | get(key)    |
      
<br/>    

- Set
  - contains 메소드로 값의 존재 여부만 확인할 수 있어 특정 요소를 get하려면 iterator를 통해 얻어야 함
- Map
  - key값을 통해 해당하는 value를 바로 얻을 수 있음

<br/>    
 
|  |  Hash   |  Tree   |
|--|-----|-----|
| 순서 |  순서 없음   | 정렬 순서 유지    |
| 시간 복잡도 | O(1)    | O(log n)    |
                                
<br/>    

- Hash와 Tree는 전혀 다른 내부 구조를 띄고 있기 때문에 시간 복잡도가 다르다.

- Hash : 순서를 유지하지 않는 대신 빠른 시간을 보장
- Tree : 트리 구조를 통해 순서를 유지하기 때문에 약간 시간이 느림

<br/>

{: .prompt-tip }
> HashSet :  속도가 빠르고, Value만 존재, 존재 여부만 판별 가능  
> HashMap : 속도가 빠르고, Key·Value 존재, get 가능  
> TreeSet : 정렬 순서 유지, Value만 존재, 존재 여부만 판별 가능  
> TreeMap : 정렬 순서 유지, Key·Value 존재, get 가능  

<br/>
<br/>

![스크린샷 2023-02-14 오후 1 55 32](https://user-images.githubusercontent.com/109974940/218642921-f3f8c43e-a3f4-4625-bc05-aad8aa2cd7bb.png)

<br/>
<br/>

---

(참고)

- [[Java] HashSet, HashMap, TreeSet, TreeMap 정리](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=eguswhd&logNo=221909757781)
- [[이것이자바다] chapter 15. 컬렉션 - 검색 기능을 강화시킨 컬렉션 TreeSet, TreeMap](https://colinch4.github.io/2021-06-11/Collection_4/)

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>

<!--

❤️면접예상질문 ❤️

-->

