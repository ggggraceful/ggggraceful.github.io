---
title: /Java/ 💚 JVM의 스택과 힙메모리 영역
author: ggggraceful
date: 2023-01-19
categories: [03.STUDY, Java]
tags: [STUDY]
---

<br/>
<br/>

## JVM의 메모리 할당 방식

---

JVM은 기본적으로 Stack Memory 와 Heap Memory 라 불리는 두가지 저장 공간을 이용해 메모리를 할당한다.  
이들에 메모리를 할당하는 방법은 바이트 코드를 한 줄 한 줄 읽는 것이다.

기본적으로 코드들은 한 줄 한 줄 읽혀서 Stack이라 불리는 공간에 차곡차곡 쌓인다.  
마지막에 들어온 변수가 먼저 나간다고 해서 LIFO(Last In First Out) 구조를 가진다고도 한다.  

하지만, 모든 변수를 Stack에 저장할 수 있는 것은 아니다.  
간단한 변수인 Primitive Type의 변수들은 Stack에 저장이 가능하지만,  
복잡한 변수는 Heap 공간에 저장되고 Stack에는 해당 Heap 공간을 가리키는 변수가 저장된다.

<br/>

" 변수가 있다면 무조건 Stack에 저장되는데,  
데이터도 Stack에 저장되는 경우는 간단한 데이터인 경우이며,  
조금만 복잡해지더라도 Stack에는 변수의 주소값만 저장되고 실제 데이터는 Heap 영역에 저장된다. "

<br/>
<br/>

## JVM의 스택 영역의 특징

---

- 정적으로 할당된 메모리 영역

- 각 스레드마다 하나씩 존재하고 스레드가 시작될 때 생성된다.

- 변수의 기본형 타입(Primitive 타입) (boolean, char, short, int, long, float, double) 의 데이터가
값이랑 같이 할당된다.

- int, long, boolean 등 기본 자료형을 생성할 때 저장하는 공간으로,  
  임시적으로 사용되는 변수나 정보들이 저장되는 영역

- 쓰레드 별로 1개만 생성된다.
  - 하나의 쓰레드는 내부적으로 static, stack, heap 영역을 갖게 됩니다.
    → 그래서 A쓰레드는 다른 쓰레드에 접근할 수는 없지만,  
      static과 heap 영역을 공유하여 사용할 수 있습니다.

- 메소드가 호출될 때마다 생성하고,  
  메서드 실행이 끝나면 pop되어 제거됩니다.

<br/>

![스크린샷 2023-01-21 오후 12 36 29](https://user-images.githubusercontent.com/109974940/213841846-09c02faa-738c-4887-ae00-37a30846d70b.png)

<br/>

![스크린샷 2023-01-21 오후 12 37 20](https://user-images.githubusercontent.com/109974940/213841870-732c0111-0928-4a16-bc32-dd110c9a3dc9.png)

<br/>
<br/>

## JVM의 힙메모리 영역의 특징

---

- 동적으로 할당된 메모리 영역

- 모든 스레드가 공유하는 영역으로  
  프로그램을 실행하면서 생성된 모든 인스턴스 또는 객체를 저장하는 공간

- "new"를 사용하여 객체를 만들 때 저장된다.

```java
Instance instance = new Instance();  -> heap에 존재
```

- Heap 영역에 생성된 Object 타입의 데이터의 참조 값이 할당된다.

- 참조형(class, interface, enum, Array 등) 자료형도 같이 저장된다.

- 힙의 참조 주소는 "스택"이 갖고 있고 해당 객체를 통해서만 힙 영역에 있는 인스턴스를 핸들링할 수 있다.

- GC가 정리하기 전까지는 남아있습니다.

<br/>
<br/>

### 힙메모리의 한계점

---

Stack은 좁은 메모리 공간이지만, Heap은 넓은 메모리 공간이다.   

Stack 메모리에 값을 할당하고 해제하는 것은 많은 비용이 들지 않지만,   
Heap 메모리에 값을 할당하고 해제하는 것은 많은 비용을 요한다.   

따라서 너무 Heap에 데이터를 자주 할당하고 해제하는 방식으로 코드를 짠다면   
같은 방식을 Stack에 했을 때보다 수십배의 속도 차이가 날 수 있다.   

이 점을 유의하면서 Heap을 사용할 때는 이 점을 유의해서 코드를 짜도록 해야한다. 


<br/>
<br/>

---

(참고링크)

- [[JAVA] JAVA 메모리 이야기 - Stack 과 Heap](https://devkingdom.tistory.com/226)
- [[Java] 메모리 구조 메소드(Method), 스택(Stack), 힙(Heap) 영역에 대하여](https://coding-factory.tistory.com/830)
- [JVM의 Memory 할당 방식 : Stack과 Heap Memory가 동작하는 방법](https://kotlinworld.com/310)
- [JVM의 Runtime Data Area](https://www.holaxprogramming.com/2013/07/16/java-jvm-runtime-data-area/)
- [[JAVA] ☕ 그림으로 보는 자바 코드의 메모리 영역(스택 & 힙)](https://inpa.tistory.com/entry/JAVA-%E2%98%95-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EB%B3%B4%EB%8A%94-%EC%9E%90%EB%B0%94-%EC%BD%94%EB%93%9C%EC%9D%98-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EC%98%81%EC%97%AD%EC%8A%A4%ED%83%9D-%ED%9E%99)

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>


<!--

❤️면접예상질문 ❤️

-->
