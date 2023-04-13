---
title: /Java/ Java가 컴파일되는 과정
author: ggggraceful
date: 2023-01-18
categories: [03.STUDY, Java]
tags: [study]
---

<br/>
<br/>

## Java가 컴파일되는 과정

---

1. 개발자가 .java 파일을 생성한다.
2. build를 한다.
3. java compiler의 javac의 명령어를 통해 바이트코드(.class)를 생성한다.
4. Class Loader를 통해 JVM 메모리 내로 로드(및 링크)하여  
   런타임 영역인 JVM 메모리에 올린다.
6. JVM에 올라온 바이트 코드들을 명령어 단위로 하나씩 가져와 실행한다.  
7. 실행엔진을 통해 컴퓨터가 읽을 수 있는 기계어로 해석된다.  
   (각 운영체제에 맞는 기계어)  
   (해당 .class파일은 기계어로 번역되게 되는 과정을 거친다.)

![사진](https://user-images.githubusercontent.com/109974940/213313682-553dcd7a-56e3-4995-8a94-3483e5be90e0.png)

<br/>

{: .prompt-info }

✔️ 자바 컴파일러(Java compiler)  
자바 컴파일러는 자바를 가지고 작성한 자바 소스 코드를 자바 가상 머신이 이해할 수 있는 자바 바이트 코드로 변환한다.
자바 컴파일러는 자바를 설치하면 javac.exe라는 실행 파일 형태로 설치된다.

<br/>

{: .prompt-info }

✔️ 자바 바이트 코드(Java bytecode)  
자바 바이트 코드(Java bytecode)란 자바 가상 머신이 이해할 수 있는 언어로 변환된 자바 소스 코드를 의미한다.
자바 컴파일러에 의해 변환되는 코드의 명령어 크기가 1바이트라서 자바 바이트 코드라고 불리고 있다.
이러한 자바 바이트 코드의 확장자는 .class이다.
자바 바이트 코드는 자바 가상 머신만 설치되어 있으면, 어떤 운영체제에서라도 실행될 수 있다.

<br/>

{: .prompt-info }

✔️ 자바 가상 머신(JVM)  
자바 가상 머신(JVM, Java Virtual Machine)이란 자바 바이트 코드를 실행시키기 위한 가상의 기계라고 할 수 있다.
자바로 작성된 모든 프로그램은 자바 가상 머신에서만 실행될 수 있으므로, 자바 프로그램을 실행하기 위해서는 반드시 자바 가상 머신이 설치되어 있어야 한다.

<br/>
<br/>

---

(참고)

- [..](https://yang-droid.tistory.com/48)
- [신입 개발자 기술면접 질문 정리 - 자바](https://dev-coco.tistory.com/153)

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>

<!--

❤️면접예상질문 ❤️

-->
