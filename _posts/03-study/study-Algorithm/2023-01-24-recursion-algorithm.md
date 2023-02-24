---
title: /Algorithm/ 💬 재귀 알고리즘
author: ggggraceful
date: 2023-01-24
categories: [03.STUDY, Algorithm]
tags: [STUDY]
---

<br/>
<br/>

## 재귀란?

---

어떤 사건이 자기 자신을 포함하고 있거나 또는 자기 자신을 사용하여 정의하고 있을 때  
이를 재귀적(recursive)이라고 한다.

<br/>
<br/>

## 팩토리얼 구하기(n!)

---

factorial

{: .prompt-tip }
> 팩토리얼(n!)
> • 0! = 1  
> • n > 0이면 n! = n × (n — 1)!

<br/>

```java
10! = 10 x 9!
 9! =  9 x 8!
```

```java
/*
  팩토리얼값을 재귀적으로 구함
 */
static int factorial(int n) {
  if (n > 0)
    return n * factorial(n - 1);
  else
    return 1; 
}

/*
  팩토리얼값을 조건 연산자를 사용하여 구현
 */
return (n > 0) ? n * factorial(n - 1) : 1;
```

<br/>

{: .prompt-warning }
>‘팩토리얼값을 구하는 예’는 재귀의 원리를 이해하기에는 좋지만  
> 효율적인 알고리즘은 아니다. 

<br/>
<br/>

### 재귀 호출

---

- ‘자기 자신과 똑같은 메서드’를 호출

factorial 메서드는  
n - 1의 팩토리얼값을 구하기 위해 다시 factorial 메서드를 호출한다.  
이러한 메서드 호출 방식을 재귀 호출(recursive call)이라고 한다. 


<br/>

### 직접재귀와 간접재귀

---

- 직접(direct) 재귀 
  : 자신과 동일한 메서드를 호출다( a ).

- 간접(indirect) 재귀는 
  : 메서드 a가 메서드 b를 호출하고,  
    다시 메서드 b가 메서드 a를 호출하는 구조( b ).

![스크린샷 2023-01-25 오후 12 00 50](https://user-images.githubusercontent.com/109974940/214470826-ff9bab03-ddb3-4ef5-afef-17a3e9f039d5.png)

<br/>

## 1-3. 유클리드 호제법

---

두 정수의 최대공약수(greatest common divisor)를 재귀적으로 구하는 방법

컴퓨터를 이용해 최대공약수를 찾을 때는, 소인수분해를 하기 보다는   
유클리드 호제법이라는 알고리즘(문제를 풀기 위해 정해진 절차)를 사용하는 것이 더 빠르다.

<br/>

![스크린샷 2023-01-25 오후 1 07 33](https://user-images.githubusercontent.com/109974940/214477648-0dd0cf6c-07b4-458c-a0a4-affa9f42c678.png)

<br/>

{: .prompt-tip }
> 최대공약수: gcd(a,b)  
> 최소공배수: lcm(a,b)  
> a, b로 나눈 몫 Q, 나머지 R  
> gcd(a,b) = gcd(b,R)
> ex) gcd (60, 24) = gcd (24 ,12) = 12  
> 　  
> • y = 0일 때 최대공약수: x  
> • y ≠ 0일 때 최대공약수: gcd(y, x % y)  
> ![스크린샷 2023-01-25 오후 1 13 00](https://user-images.githubusercontent.com/109974940/214478171-61f6a1de-0c23-4831-b575-9d4ab645b3d3.png)

<br/>

```java
// 정수 x, y의 최대공약수를 구하여 반환
static int gcd(int x, int y) {
   if (y == 0)
     return x;
   else
    return gcd(y, x % y);
}
```

<br/>
<br/>

# 2. 재귀 알고리즘 분석

---

<br/>

## 2-1. 재귀 알고리즘 분석하기

<br/>

### 하향식 분석

<br/>

{: .prompt-tip }
> ✔️ recur(3)의 호출
> ..

<br/>

### 상향식 분석

<br/>

## 2-2. 재귀 알고리즘의 비재귀적 표현

<br/>

### 꼬리 재귀의 제거

<br/>

### 재귀의 제거

<br/>

## 2-3. 메모화


<br/>
<br/>

# 3. 하노이의 탑

---



<br/>
<br/>

# 4. 8퀸 문제

---

<br/>

## 4-1. 퀸 배치하기

<br/>


## 4-2. 분기 조작

<br/>

## 4-3. 분기 한정법

<br/>

## 4-4. 8퀸 문제를 해결하는 프로그램 만들기


<br/>
<br/>



---

(참고)

- 두잇! 알고리 기초
- [재귀알고리즘 분석](https://edwardmoon.tistory.com/105)
- [재귀함수와 꼬리 재귀](https://velog.io/@dldhk97/%EC%9E%AC%EA%B7%80%ED%95%A8%EC%88%98%EC%99%80-%EA%BC%AC%EB%A6%AC-%EC%9E%AC%EA%B7%80)
- [정수론 (1) - 최대공약수, 최소공배수, 유클리드 호제법](https://dimenchoi.tistory.com/46)
- [최대공약수와 최소공배수](https://post.naver.com/viewer/postView.nhn?volumeNo=6788621&memberNo=15932120)

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>

<!--

❤️면접예상질문 ❤️

-->

