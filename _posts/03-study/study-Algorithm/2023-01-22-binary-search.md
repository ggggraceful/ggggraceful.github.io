---
title: /Algorithm/ 이분탐색, 이분탐색의 시간복잡도
author: ggggraceful
date: 2023-01-22
categories: [03.STUDY, Algorithm]
tags: [study, algorithm]
---

<br/>
<br/>

## 1. 이분탐색

---

- 중간값과 찾으려는 값의 대소를 비교한 뒤  
  탐색 범위를 반으로 줄여가며 값을 찾는 탐색 알고리즘

- 찾고자 하는 값이 정렬된 배열의 중간 값보다 크면  
  중간값을 포함한 하위 값들은 탐색 대상에서 제외된다. 
- 반대로 찾고자 하는 값이 배열의 중간 값보다 작으면  
  중간 값을 포함한 상위 값들은 탐색에서 제외된다.

<br/>

- 장점
  - 처음부터 끝까지 돌면서 탐색하는 것보다 훨씬 빠르다.

- 단점
  - 배열의 중간을 기준으로 데이터를 탐색하기 때문에  
    반드시 ```데이터가 정렬된 상태```로 존재해야 한다.

<br/>
<br/>
<br/>

## 2. 이분탐색의 시간복잡도

---

이분탐색의 시간복잡도는 logN으로
배열을 전수조사하는 O(N)에 비하면 상대적으로 빠른 탐색 알고리즘에 속한다.

<br/>
<br/>

### 🔸이분탐색과 선형검색의 시간복잡도 코드

---

<br/>

```java
/*
 이분탐색의 시간복잡도
 */
static int binSearch(int[] a, int n, int key) {
    int pl = 0; // 검색 범위 첫 인덱스
    int pr = n –1; // 검색 범위 끝 인덱스

    do {
        int pc = (pl + pr) / 2; // 중앙 요소의 인덱스
        if (a[pc] == key)
          return pc; // 검색 성공!
        else if (a[pc] < key)
          pl = pc + 1; // 검색 범위를 뒤쪽 절반으로 좁힘
        else
          pr = pc – 1; // 검색 범위를 앞쪽 절반으로 좁힘
  } while (pl <= pr);
	
  return –1; // 검색 실패!
}
```

```java
/*
  선형검색의 시간복잡도
 */
static int seqSearch(int[] a, int n, int key) {
int i = 0;
while(i < n) {
 if(a[i] == key)
 return i; // 검색 성공! 
 i++;
}
return –1; // 검색 실패!
}
```

<br/>
<br/>

### 🔸시간복잡도 계산법

---

![계산법](https://user-images.githubusercontent.com/109974940/214263943-c11e258f-cd21-4748-ad52-9c77f686e118.png)

<br/>
<br/>
<br/>


---

(참고)

- [[Algorithm] 이진 탐색 (이분 탐색, Binary Search) 코드와 시간 복잡도](https://kangworld.tistory.com/65)

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>

<!--

❤️면접예상질문 ❤️

-->


