---
title: /Java/ Entity에서 필드나 컬럼의 길이제한 해주는 어노테이션
author: ggggraceful
date: 2023-04-06
categories: [03.STUDY, Java]
tags: [STUDY]
---

<br/>
<br/>

# @Column(length = value)

---

<br/>

```java
import javax.validation.constraints.Size;
  
public class Post {
	
  @Column(length = 20)
  private String title;
  
}
```

<br/>

- length 옵션 추가
- 해당 부분은 유효성 검사는 하지 않음

- Entity로 db를 생성할때 사용
- SQL Column 길이를 설정하는 데 사용
  > (예시)  
  > 해당 colum이 VARCHAR(20) 타입으로 생성되고,  
  > 20보다 긴 문자열을 넣으려고 하면 SQL Error 발생  

<br/>
<br/>

# @Length

---

<br/>

```java
import org.hibernate.validator.constraints.Length;

public class Post {

	@Column
  @Length(min = 3, max = 20)
  private String title;

}
```

<br/>

- 유효성 검사를 해줌
- Hibernate Validation 어노테이션


<br/>
<br/>

# @Size

---

<br/>

```java
import javax.validation.constraints.Size;

public class Post {

	@Column
  @Size(min = 3, max = 20)
  private String title;

}
```

<br/>

- 유효성 검사를 해줌
- Bean Validation 어노테이션
- JPA와 Hinernate로부터 독립적인 bean을 만들어 줌

- 문자열, 배열 등의 크기를 검증하는 데 사용


<br/>
<br/>

# @Max, @Min

---

<br/>

- 숫자를 사용하는 필드 검증
- String(숫자 표시), int, byte 등의 최대 길이 체한








<br/>
<br/>

---

(참고)

- ..

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>

<!--

❤️면접예상질문 ❤️

-->

