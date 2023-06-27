---
title: 🔍 application.yml 분리
author: ggggraceful
date: 2023-06-27
categories: [06.HOW TO USE]
tags: [how to use]
---

<br/>
<br/>

## 방법 1

---

<br/>

설정을 한 applicaiton.yml 에서 이러한 방식으로 분리해 주는 방식과

<br/>

```java
# version 1
server:
  port: 8080

  ...

---
# version 2
server:
  port: 8080

	...
```

<br/>
<br/>


## 방법 2

---

<br/>

다음과 같이 profile 단위로 파일 자체를 분리하는 방식이 있다.

- application.yml
- applivation-dev.yml
- applivation-test.yml

<br/>

분리 후 적용할 프로파일을 설정해 주어야 한다.

<br/>

그러려면 intellij에서 구성 편집에 들어가

활성화된 프로파일에 내가 적용할 application.yml을 입력해주면된다.

<br/>

applivation-dev.yml를 사용하고 싶다면

dev라고 입력해주면

해당 프로파일이 적용되 실행될 것이다!


<br/>
<br/>
