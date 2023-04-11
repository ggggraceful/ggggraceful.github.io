---
title: ✨TIL - 게시물 삭제시 댓글도 함께 삭제 구현
author: ggggraceful
date: 2023-04-11
categories: [06.HOW TO USE]
tags: [how to use]
---

<br/>
<br/>

# 삭제

---

<br/>

삭제했다고 해주고   
복구를 위해 보관해 놓았다가  
일정 기간이 지났을 경우에는 Cascade를 사용해 삭제  

<br/>
<br/>

# Cascade

---

<br/>

생명주기를 공유하는(어느 한 엔티티의 생명주기 의존) 엔티티들이 존재할 경우 Cascade를 사용하면 좋다.  
게시판이 제거됨과 동시에 그 안에 존재하는 게시글, 댓글 (혹은 추천)이 모두 제거될 것이다.

<br/>

단방향 매핑으로 사용이 가능할 경우 양방향 매핑을 전혀 사용할 필요가 없다.

<br/>

하지만 우리가 Cascade를 사용할 경우  
즉 @ManyToOne 어노테이션의 표현으로만 충분히 매핑이 가능한데도 불구하고  
@OneToMany 어노테이션을 활용하고 불필요한 양방향 매핑을 사용하게 된다.  

<br/>

예를들어 댓글 아래에 대댓글을 달고 이러한 식으로 꼬리를 무는 형식을 지칭하는데  
이러한 부분은 1:N의 관계로 표현이 가능하다.  
이러한 부분에 있어서는 양방향 매핑이 필요하다.  

<br/>

- JPA에 의해 처리되어 JPA에 의해 외래 키를 찾아가며 참조하는 레코드를 제거
- 여러개의 쿼리사용해 제거

<br/>
<br/>

# @Delete

---

<br/>

Cascade와 같은 효과
```java
@OnDelete(action = OnDeleteAction.CASCADE)
```

<br/>

- 불필요한 연관관계 매핑을 제거해주고 연관관계를 제거
- DB에 의해 직접 처리
- 단일 쿼리를 통해 연쇄적으로 제거

<br/>
<br/>

# 구현

---

<br/>

post를 삭제하면  
해당 post의 자식인 comment들이 모두 삭제되고  
해당 post가 삭제됨

<br/>

```java
@Builder
@Entity
@Getter
@NoArgsConstructor
@AllArgsConstructor
public class Post extends BaseTimeEntity {


  ...

  @OneToMany(fetch = LAZY, //  CascadeType를 사용하기 위해 추가
          mappedBy = "post",
          cascade =  {CascadeType.PERSIST, CascadeType.REMOVE}) // 부모 엔티티를 삭제하면 자식 엔티티 삭제
  private List<Comment> comment = new ArrayList<>();

  ...
}
```

```java
@Entity
@Builder
@Getter
@NoArgsConstructor
@AllArgsConstructor
public class Comment extends BaseTimeEntity {

  ...

  @ManyToOne(fetch = FetchType.LAZY)
  @JoinColumn(name = "post_id", nullable = false)
  private Post post; // mappedBy에 같은 이름으로 넣어주어야함

  ...
  
}
```


<br/>
<br/>

---

(참고)

- [Cascade vs @Delete](https://gilssang97.tistory.com/71)

