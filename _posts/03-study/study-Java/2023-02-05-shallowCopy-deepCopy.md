---
title: /Java/ 깊은복사, 얕은복사
author: ggggraceful
date: 2023-02-05
categories: [03.STUDY, Java]
tags: [study]
---

<br/>
<br/>

# 0. 배열의 깊은 복사, 얕은 복사

---

- Java의 복사
  1. 얕은 복사(Shallow copy):  
     원본 배열이나 복사된 배열이 변경될 때 상대 배열의 값이 같이 변경된다.
  2. 깊은 복사(Deep copy):  
     원본 배열이나 복사된 배열이 변결될 때 서로간의 값은 바뀌지 않는다.

<br/>

- primitive type의 변수:  
  얕은 복사로도 문제 없이 진행된다.
- reference type(객체, 배열 등)의 변수:  
  깊은 복사를 사용해야지만 객체의 실제 데이터를 복사할 수 있다.

<br/>
<br/>

# 1. 얕은 복사(Shallow Copy)

---

<br/>

- 정의: 주소값이 복사되는 것을 말한다.
- 장점
  - 같은 객체를 공유하므로 메모리를 절약하고, 빠르다.  
    (참조에 의한 호출(Call By Reference)에서 얕은 복사가 이루어 지는 이유 중 하나)
- 단점
  - 두 개 이상의 객체가 같은 대상을 가르키고 있기 때문에,  
    의도치 않게 여러 개의 객체가 동시에 수정될 수 있다.

<br/>

![얕은복사](https://user-images.githubusercontent.com/109974940/216811405-33775342-fef8-4d8a-b0b4-9d5b2a3dd7df.png)

<br/>

```java
int[] a = {1, 2, 3, 4};
int[] b = a;
System.out.println(Arrays.toString(a)); // [1, 2, 3, 4]

System.out.println(Arrays.toString(b)); // [1, 2, 3, 4]


// 원본 배열 값 변경

a[1] = 10;
System.out.println(Arrays.toString(a)); // [1, 10, 3, 4]

System.out.println(Arrays.toString(b)); // [1, 10, 3, 4]


// 복사한 배열 값 변경

b[3] = 1111;
System.out.println(Arrays.toString(a)); // [1, 10, 3, 1111]

System.out.println(Arrays.toString(b)); // [1, 10, 3, 1111]
```

얕은 복사에서는 =연산자를 사용해 해당 변수에 담겨있는 값을 복사한다. 배열의 경우 해당 변수에 heap의 데이터를 가리키는 참조값이 저장되어있기 때문에 참조값이 복사되어 같은 원본 배열을 가리키게 되는 것이다.

<br/>
<br/>

# 2. 깊은 복사(Deep Copy)

---

<br/>

- 정의: 새로운 메모리 공간에 값(Value)을 복사하는 것이다.
- 장점
  - 여러 객체가 동시에 수정되는 일이 발생하지 않아, 변경에는 안전하다.
- 단점
  - 객체 생성 비용이 비싸며, 메모리를 많이 점유한다.
  - 특정 객체를 깊은 복사하는 경우 Clonable 인터페이스를 활용하여,  
    clone()메소드를 Overring 해주어야 깊은 복사가 가능하다.

<br/>

![깊은복사](https://user-images.githubusercontent.com/109974940/216811370-cf45a330-96df-4159-820b-acbae90e2aa6.png)

```java
int[] a = {1, 2, 3, 4};
int[] b = new int[a.length]; 
for (int i = 0; i < a.length; i++) {
    b[i] = a[i];
}
System.out.println(Arrays.toString(a)); // [1, 2, 3, 4]

System.out.println(Arrays.toString(b)); // [1, 2, 3, 4]


// 원본 배열 값 변경

a[1] = 10;
System.out.println(Arrays.toString(a)); // [1, 10, 3, 4]

System.out.println(Arrays.toString(b)); // [1, 2, 3, 4]


// 복사한 배열 값 변경

b[3] = 1111;
System.out.println(Arrays.toString(a)); // [1, 10, 3, 4]

System.out.println(Arrays.toString(b)); // [1, 2, 3, 1111]
```

이렇게 for문을 이용해 복사를 하는 방법도 있지만 java에서 지원하는 다양한 메소드(method)들을 활용하면 더 편하게 깊은 복사를 할 수 있다.

- [다양한 복사 메서드 참고](https://seoyoung2.github.io/java/2021/01/21/java-copy.html)

<br/>
<br/>

---

(참고링크)

- [[Java] 깊은복사와 얕은복사(Call By Value & Call By Reference)](https://kyhyuk.tistory.com/182)
- [
  [java] 배열의 얕은 복사, 깊은 복사](https://seoyoung2.github.io/java/2021/01/21/java-copy.html]
)

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>

<!--

❤️면접예상질문 ❤️

-->

