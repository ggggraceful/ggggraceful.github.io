---
title: 🔍 isPresent(), isEmpty()
author: ggggraceful
date: 2023-04-05
categories: [06.HOW TO USE]
tags: [how to use]
---

<br/>
<br/>

코드를 작성하다보니 isPresent()와 isEmpty()의 차이가 궁금해 졌다.  
차이는 별거 없었다..  

<br/>
<br/>

{: .prompt-tip }
> isPresent() <-> isEmpty() : java11 에서 처음 사용

<br/>
<br/>

# isPresent()

---
<br/>

```java

if (emailOptional.isPresent()) 
	throw new MemberInfoNotExistException();

```

<br/>

- null이 아닌 경우 다음 코드 실행


아래처럼 조건문에 이름이 존재하는지 안 한는지 체크하는 경우   
내부 로직을 타기 전 오류가 나기 쉬운데,
변수를 선언한 다음에 변수에 대한 null검사를 하는 것을 잊어버릴 수 있기 때문
따라서 아래와 같은 코드는 nullPointException처리가 날 확률이 높다.

```java

if(name != null) {
    System.out.println(name.length());
}

```

<br/>
<br/>


# isEmpty()

---

<br/>

```java

if (emailOptional.isEmpty()) 
	throw new MemberInfoNotExistException();

```

<br/>
<br/>



