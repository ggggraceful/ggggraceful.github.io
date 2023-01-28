---
title: 📒 알고리즘 제어문
author: ggggraceful
date: 2023-01-25
categories: [04.AlGORITHM]
tags: [STUDY]
---

<br/>
<br/>

# 1. 조건문

---

<br/>
<br/>

## 1-1. if문

---

### if~else문

- if문은 조건에 따라 두 대의 문장중에 하나가 수행되는 조건문

```
if(조건식)
    실행 문장1;
else
    실행 문장2;
```

### if ~ else if문

- if ~ else if문은 if문을 이용하여 다중 선택을 가능하게 해준다.

```
if(조건식1)
    실행 문장1;
else if(조건식2)
    실행 문장2;
...
else
    실행 문장3;
```

처음 조건식이 참으로 평가되면 해당 식을 수행한 후, if문장을 빠져 나가게 된다. 처음 조건절이 거짓으로 평가되면 계속해서 else if 조건절을 평가하여 수행한다.

<br/>
<br/>

## 1-2. switch

---

### switch ~ case문

```java
switch(수식) {
    case 값1:
        실행 문장1;
       break;
    case 값2:
         실행 문장2;
        break;
  .....
   case 값n:
        실행 문장n;
        break;
   defulat:
        디폴트 실행 문장;
}
```
### 중첩된 switch문

```java

```
<br/>
<br/>

# 2. 반복문

---

<br/>
<br/>

# 분기문

---

<br/>
<br/>





## while문

---

- 사전판단반복

```java
while (제어식) 명령문
```

```java
/*
 while 문으로 1, 2, …, n의 합을 구함
 */
  int sum = 0; // 합 
  int i = 1;
  
  while (i <= n) { // i가 n 이하면 반복함
  sum += i; // sum에 i를 더함
  i++; // i값을 1만큼 증가시킴
  }
```

<br/>
<br/>

## for 문 반복

---

- 하나의 변수를 사용하는 반복문은 while 문보다 for 문을 사용하는 것이 좋음

```java
for (초기화 부분; 제어식; 업데이트 부분) 명령문
```

```java
/* 
for 문으로 1, 2, …, n의 합을 구함
 */
 int sum = 0; // 합 
   for (int i = 1; i <= n; i++)
   sum += i; // sum에 i를 더함
```
<br/>
<br/>

## do

---

```java
/*
양수만 입력하여 1, 2, …, n의 합을 구함
 */

//n이 0보다 클 때까지 반복합니다
 do {
   System.out.print("n값: ");
   n = stdIn.nextInt();
   } while (n <= 0);
```
<br/>
<br/>

## if

---

<br/>
<br/>


---

(참고)

- 두잇
- [Java 제어문(Control statement)의 조건문(Conditional statement)](https://www.devkuma.com/docs/java/conditional-statement/#switch--case%EB%AC%B8)

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>
