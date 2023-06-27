---
title: /Data structure/ 💬 Priority Queue, Heap
author: ggggraceful
date: 2023-03-02
categories: [03.STUDY, Data structure]
tags: [study, data structure]
---

<br/>
<br/>

{: .prompt-tip }
> ✔️ 큐(Queue)    
> : 먼저 들어오는 데이터가 먼저 나가는 FIFO(First In First Out) 형식의 자료구조  
> ✔️ 우선순위 큐(Priority Queue)  
> : 먼저 들어오는 데이터가 아니라, 우선순위가 높은 데이터가 먼저 나가는 형태의 자료구조,  
>   우선순위 큐는 일반적으로 힙(Heap)을 이용하여 구현,   
>   배열과 연결리스트를 이용해서도 구현가능

<br/>
<br/>

# 힙(Heap)

---

- 힙(Heap)은 우선순위 큐를 위해 고안된 `완전이진트리` 형태의 자료구조  
  - [이 블로그의 다른글- 트리](https://ggggraceful.github.io/posts/tree/)
- 여러 개의 값 중 최댓값 또는 최솟값을 찾아내는 연산이 빠름

<br/>
<br/>

# 힙의 특징

---

<br/>

- 완전이진트리 형태로 이루어짐
- 부모노드와 서브트리간 대소 관계가 성립됨 (반정렬 상태)
- 이진탐색트리(BST)와 달리 중복된 값이 허용

<br/>
<br/>

# 힙의 종류

---

<br/>

- 최대 힙 (Max Heap)  
: 부모 노드의 키 값이 자식 노드보다 크거나 같은 완전이진트리  
  key(부모노드) ≥ key(자식노드)  

<br/>

![스크린샷 2023-03-02 오후 3 52 49](https://user-images.githubusercontent.com/109974940/222353139-0dd0e555-10dc-4c8c-ac45-569fd5ee09d1.png)

<br/>

- 최소 힙 (Min Heap)  
: 부모 노드의 키 값이 자식 노드보다 작거나 같은 완전이진트리  
  key(부모노드) ≥ key(자식노드) 

<br/>

![스크린샷 2023-03-02 오후 3 53 07](https://user-images.githubusercontent.com/109974940/222353193-82667357-01e0-4aa8-b218-4bbd0a72c169.png)

<br/>

# 선순위 큐 구현방법 비교

---

- 배열과 연결리스트
  - 선형 구조의 자료구조
  - 삽입 또는 삭제 연산을 위한 시간복잡도는 O(n)

- 힙트리
  - 완전이진트리 구조
  - 힙트리의 높이는 log₂(n+1)
  - 힙의 시간복잡도는 O(log₂n)


| 구현방법       | 삽입       | 삭제  |
|------------|----------|-----|
| 순서없는 배열    | O(1)     |  O(n)   |
| 순서없는 연결리스트 | O(1)     | O(n)    |
| 정렬된 배열     | O(n)     |  O(1)     |
| 정렬된 연결리스트  | O(n)     |   O(1)    |
| 힙          | O(log₂n) | O(log₂n) |


# 우선순위 큐 ADT

---

<br/>




<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

---

(참고)

- [우선순위 큐와 힙 (Priority Queue & Heap)](https://suyeon96.tistory.com/31)
- 

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>

<!--

❤️면접예상질문 ❤️

-->

