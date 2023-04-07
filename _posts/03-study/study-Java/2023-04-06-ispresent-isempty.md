---
title: /Java/ isPresent(), isEmpty(), 
author: ggggraceful
date: 2023-04-06
categories: [03.STUDY, Java]
tags: [STUDY]
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

---

(참고)

- [..](../../../..)

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>

<!--

❤️면접예상질문 ❤️

-->

