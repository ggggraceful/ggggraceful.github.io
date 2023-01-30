---
title: /OS/ 동시성, 병렬성
author: ggggraceful
date: 2023-01-23
categories: [03.STUDY, OS]
tags: [STUDY]
---

<br/>
<br/>

![스크린샷](https://user-images.githubusercontent.com/109974940/214333716-54d75fee-64bd-4373-ad40-947d2fddf1b9.png)


<br/>
<br/>

# 동시성과 병렬성

---

<br/>

| 동시성(Concurrency)                                       | 병렬성(Parallelism)                                                           |
|---------------------------------------------|-----------------------------------------------------------------|
| 논리적인 개념                                     | 물리적인 개념                                                         |
| 병렬성을 가능하게 함                                 | 동시성의 하위집합                                                       |
| 작업이 빠르게 번갈아가며 실행되기에<br/>동시에 실행되는 것 같이 보이는 것 | 실제로 동시에 여러 작업이 처리되는 것                                           |
| 싱글 코어에서<br/>멀티 쓰레드(Multi thread)를 동작 시키는 방식 | 멀티 코어에서 멀티 쓰레드(Multi thread)를 동작시키는 방식<br/>(= 멀티코어 프로세서 구조와 같음) |
| 하나의 코어만 필요                                  | 최소 2개의 코어 필요                                                    |
| 한번에 많은 것을 처리                                | 한번에 많은 일을 처리                                                    |
| 소프트웨어 설계에 관한 것                              | 하드웨어에 관한 것                                                      |


<br/>
<br/>

# 스레드 동기화 문제
---

레이스 컨디션(Race Condition)
교착 상태(Deadlock)
기아 상태(Starvation)
라이브락(Livelock)
---

(참고)

- [동시성(Concurrency) vs 병렬성(Parallelism)](https://seamless.tistory.com/42)
- [Concurrency vs Parallelism](https://www.codeproject.com/Articles/1267757/Concurrency-vs-Parallelism)
- [[OS] 스레드 동기화 문제 - Race Condition, Deadlock, Starvation, Livelock](https://cheetile.tistory.com/entry/OS-%EC%8A%A4%EB%A0%88%EB%93%9C-%EB%8F%99%EA%B8%B0%ED%99%94-%EB%AC%B8%EC%A0%9C-Race-Condition-Deadlock-Starvation-Livelock)

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>

<!--

❤️면접예상질문 ❤️

-->

