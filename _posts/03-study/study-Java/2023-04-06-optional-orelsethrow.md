---
title: /Java/ isPresent()를 orElseThrow()로 바꾸기
author: ggggraceful
date: 2023-04-06
categories: [03.STUDY, Java]
tags: [STUDY]
---

<br/>
<br/>

# isPresent() 사용

```java
	private Member getMemberIfExists() {

		// 이미 생성되어 있는 SecurityUtil에 getCurrentUsername()를 가입된 이메일인지 검증하기 위해 사용
		Optional<String> emailOptional = SecurityUtil.getCurrentUsername();

		if (emailOptional.isPresent()) { // 객체 존재여부를 확인

			String email = emailOptional.get();
			Optional<Member> memberOptional = memberRepository.findByEmail(email);

			// 가입한 멤버가 아닐 경우2 : 비어 있을 때
			if (memberOptional.isEmpty()) {
				throw new MemberInfoNotExistException();
			} else return memberOptional.get();

		// 가입한 멤버가 아닐 경우1 : 존재하지 않을 때
		} else throw new MemberInfoNotExistException();
	}
```

<br/>
<br/>

# orElseThrow() 사용

```java
	private Member getMemberIfExists() {

  // 현재 로그인한 사람이 있을 경우 해당 회원의 email을 가져온다.
  String email = SecurityUtil.getCurrentUserEmail().orElseThrow(()
  -> new MemberInfoNotExistException());

  // mysql에서 해당 email을 가진 회원이 없을 경우 예외발생, 있으면 회원 정보를 가져온다.
  return memberRepository.findByEmail(email).orElseThrow(()
  -> new MemberInfoNotExistException());
  }
```

<br/>
<br/>

# 람다로 변경

```java
	private Member getMemberIfExists() {

		// 현재 로그인한 사람이 있을 경우 해당 회원의 email을 가져온다.
		String email = SecurityUtil.getCurrentUserEmail().orElseThrow(MemberInfoNotExistException::new);

		// mysql에서 해당 email을 가진 회원이 없을 경우 예외발생, 있으면 회원 정보를 가져온다.
		return memberRepository.findByEmail(email).orElseThrow(MemberInfoNotExistException::new);
	}
```

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

