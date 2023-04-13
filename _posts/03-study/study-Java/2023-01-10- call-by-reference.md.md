---
title: /Java/ call by value, call by reference
author: ggggraceful
date: 2023-01-10
categories: [03.STUDY, Java]
tags: [study]
---

<br/>
<br/>

# 인수전달방법

---

함수를 호출할 때에는  
함수에 필요한 데이터를 인수(argument)로 전달해 줄 수 있다.  

이렇게 함수에 인수를 전달하는 방법에는 크게 다음과 같이 두 가지 방법이 있습니다.

<br/>

1. 값에 의한 전달(call by value)  
2. 참조에 의한 전달(call by reference)

<br/>
<br/>

## 1. call by reference 

---

(참조에 의한 전달)

<br/>

- 함수의 호출 방식 중 하나
- 메서드에서 사용되는 파라미터가 값이 아닌 (= 함수에서 인수로 변수의 값을 전달하는 대신)
  주소를 참조하여 데이터에 직접 접근할 수 있게 하는 호출 (= 주소값을 전달하는 방식)

- java는 대체적으로 call by reference
- shallow copy(얕은 복사)라고도 불린니다.

<br/>
<br/>

### 1-1. call by reference 사용

---

함수 호출시 인자로 전달되는 변수의 레퍼런스를 전달하고, (해당 변수를 가르킨다.)
함수 안에서 인자의 값이 변경되면,
아규먼트로 전달된 객체의 값도 함께 변경된다.  
(=전달받은 값을 변경할 경우 원본도 같이 변경된다.)

<br/>
reference type(참조 자료형)을 넘길 시에는    
해당 객체의 주소값을 복사하여 사용합니다.  

<br/>
원본 객체의  프로퍼티까지는 접근이 가능하나, 원본 객체 자체를 변경할 수는 없습니다.

<br/>
<br/>

### 1-2. 자바에서의 사용?

---

️자바는 (C/C++ 같이) 변수의 주소값 자체를 가져올 방법이 없고,  
이를 넘길 수 있는 방법 또한 가지고 있지 않습니다.    

<br/>
그래서 자바는 항상 call by value 로만 동작하고, Reference 값을 넘기는 것만 가능합니다.  
(인자를 전달하는 두가지 방식 : call by value, call by reference)

<br/>
<br/>

## 2. call by value

---
(값에 의한 전달 방법)

<br/>

- 인수로 전달되는 변수가 가지고 있는 값을 함수 내의 매개변수에 복사하는 방식
- 이렇게 복사된 값으로 초기화된 매개변수는  
  인수로 전달된 변수와는 완전히 별개의 변수가 됨
- 함수 내에서의 매개변수 조작은  
  인수로 전달되는 변수에 아무런 영향을 미치지 않음

- deep copy(깊은 복사)라고도 불린다. 

<br/>
<br/>

## 📎 배열의 깊은 복사, 얕은 복사

---

### [ 🌐이 블로그의 다른 글🌐 /Java/ 깊은복사, 얕은복사](https://ggggraceful.github.io/posts/shallowCopy-deepCopy/)


<br/>
<br/>

---

(참고)

- [인수 전달 방법](http://www.tcpschool.com/c/c_pointer_callBy)

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>

<!--

❤️면접예상질문 ❤️
- Call by reference란 무엇이고 보통 어떻게 쓰이나요?

-->
