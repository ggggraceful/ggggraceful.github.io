---
title: /etc/ 동기&비동기, 블록킹&논블록킹
author: ggggraceful
date: 2023-01-17
categories: [03.STUDY, etc]
tags: [STUDY]
---

<br/>
<br/>

- 동기 & 비동기 : 프로세스의 수행 순서 보장에 대한 매커니즘
  - 동기 : 작업을 동시에 수행하거나, 동시에 끝나거나, 끝나는 동시에 시작
  - 비동기 : 시작, 종료가 일치하지 않으며, 끝나는 동시에 시작을 하지 않음

![스크린샷 2023-01-18 오후 4 56 32](https://user-images.githubusercontent.com/109974940/213115016-f6a99fdb-8c1b-48a8-9009-5592da407030.png)

<br/>

- 블록킹 & 논블록킹 : 프로세스의 유휴 상태에 대한 개념
  - 블록킹 : 자신의 작업을 진행하다가 다른 주체의 작업이 시작되면  
  　　　　　다른 작업이 끝날 때까지 기다렸다가 자신의 작업을 시작하는 것
  - 논블록킹 : 다른 주체의 작업에 관련없이 자신의 작업을 하는 것

## 동기

---

Synchronous

- 서버에서 요청을 보냈을 때 응답이 돌아와야 다음 동작을 수행할 수 있는 방식  
  (A작업이 모두 진행 될때까지 B작업은 대기해야한다.)
- 요청과 결과가 한 자리에서 동시에 일어난다.
- A노드와 B노드 사이의 작업 처리 단위(transaction)를 동시에 맞춘다.

<br/>

![스크린샷 2023-01-21 오후 12 59 09](https://user-images.githubusercontent.com/109974940/213842425-80512109-7abb-41d6-80ea-ba9b3d0745ac.png)

<br/>

- 장점  
  :설계가 매우 간단하고 직관적
- 단점  
  :결과가 주어질 때까지 아무것도 못하고 대기해야 한다.

<br/>
<br/>

## 비동기

---

Asynchronous

- 반대로 요청을 보냈을 때  
  응답 상태와 상관없이 다음 동작을 수행 할 수 있는 방식  
  (A작업이 시작하면 동시에 B작업이 실행된다. A작업은 결과값이 나오는대로 출력된다.)
- 비동기적 코드의 실행 결과는  
  동기적 코드가 전부 실행 되고나서 값을 반환한다.
- 노드 사이의 작업 처리 단위를 동시에 맞추지 않아도 된다.

<br/>

![스크린샷 2023-01-21 오후 1 00 05](https://user-images.githubusercontent.com/109974940/213842452-cc38c5a0-3a65-4094-816e-aa6c8e17da00.png)


<br/>

- 장점  
  :결과가 주어지는데 시간이 걸리더라도  
   그 시간 동안에 다른 작업을 할 수 있으므로  자원들을 효율적으로 사용 할 수 있다.
- 단점  
  :동기보다 복잡한 설계

<br/>
<br/>

## 블로킹

---

Blocking

![스크린샷 2023-01-21 오후 12 56 20](https://user-images.githubusercontent.com/109974940/213842319-b3cc9942-dca0-4e7c-85d1-42c80ff33e76.png)

<br/>

1. A함수가 B함수를 호출하면 B에게 제어권을 넘긴다.
2. 제어권을 넘겨받은 B는 열심히 함수를 실행한다. A는 B에게 제어권을 넘겨주었기 때문에 함수 실행을 잠시 멈춘다.
3. B함수는 실행이 끝나면 자신을 호출한 A에게 제어권을 돌려준다.

<br/>
<br/>

## 논블로킹

---

Non-Blocking

![스크린샷 2023-01-21 오후 12 58 05](https://user-images.githubusercontent.com/109974940/213842372-0c05d84a-cfac-4d02-9ac5-c363e93bf3f5.png)

<br/>

1. A함수가 B함수를 호출하면, B 함수는 실행되지만, 제어권은 A 함수가 그대로 가지고 있는다.
2. A함수는 계속 제어권을 가지고 있기 때문에 B함수를 호출한 이후에도 자신의 코드를 계속 실행한다.

<br/>
<br/>

## 동기&비동기 + 블로킹&논블로킹 조합

---

![스크린샷 2023-01-21 오후 1 03 02](https://user-images.githubusercontent.com/109974940/213842542-11c27ac8-79e9-476e-8d49-6f8a05fc35ee.png)

<br/>
<br/>

---

(참고)

- [동기, 비동기](https://velog.io/@daybreak/%EB%8F%99%EA%B8%B0-%EB%B9%84%EB%8F%99%EA%B8%B0-%EC%B2%98%EB%A6%AC)
- [동기, 비동기 처리](https://velog.io/@daybreak/%EB%8F%99%EA%B8%B0-%EB%B9%84%EB%8F%99%EA%B8%B0-%EC%B2%98%EB%A6%AC)
- [109dev 2021. 1. 15.](https://private.tistory.com/24)
- [[Java]동기와 비동기 방식(Asynchronous processing model)](https://webheck.tistory.com/entry/Java%EB%8F%99%EA%B8%B0%EC%99%80-%EB%B9%84%EB%8F%99%EA%B8%B0-%EB%B0%A9%EC%8B%9DAsynchronous-processing-model)
- [[10분 테코톡] 🎧 우의 Block vs Non-Block & Sync vs Async](https://www.youtube.com/watch?v=IdpkfygWIMk)
- [[운영체제] 동기와 비동기, 블로킹과 논블로킹](https://cotak.tistory.com/136)
- [동기/비동기 vs 블로킹/논블로킹](https://xzio.tistory.com/2057)
- [블로킹(Blocking)과 논 블로킹(Non-Blocking)이란 무엇인가?!](https://jaehoney.tistory.com/242)
- [동기 & 비동기 / 블로킹 & 논블로킹 💯 완벽 이해하기](https://inpa.tistory.com/entry/%F0%9F%91%A9%E2%80%8D%F0%9F%92%BB-%EB%8F%99%EA%B8%B0%EB%B9%84%EB%8F%99%EA%B8%B0-%EB%B8%94%EB%A1%9C%ED%82%B9%EB%85%BC%EB%B8%94%EB%A1%9C%ED%82%B9-%EA%B0%9C%EB%85%90-%EC%A0%95%EB%A6%AC)

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>

<!--

❤️면접예상질문 ❤️

-->
