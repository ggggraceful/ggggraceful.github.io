---
title: 🔍 게시물 단일 조회 stream 사용해 구현
author: ggggraceful
date: 2023-04-11
categories: [06.HOW TO USE]
tags: [how to use]
---

<br/>
<br/>

```java
  //게시글 전체 조회
  @Transactional
  public List<AllPostResDto> getAllPost() {
    List<Post> postList = postRepository.findAll();
    return postList.stream()
        .map(AllPostResDto::new).toList();
    }
```

⬇️

```java
  //게시글 전체 조회
  @Transactional
  public List<AllPostResDto> getAllPost() {
    List<Post> postList = postRepository.findAll();
    return  postList.stream()
        .map((post) -> new AllPostResDto(post))
        .toList();
  }

```

<br/>
<br/>

```java
    // 게시글 상세 조회
    @Transactional(readOnly = true)
    public PostResponseDto getOnePost(Long id) {
        Post post = validateCheck.getPostIfExists(id);

        // 게시글 상세 조회 시 댓글도 함께 조회
        List<Comment> comments = commentRepository.findByPostId(id);
        List<CommentResDto> commentList = new ArrayList<>();
        for (Comment comment : comments) {
            commentList.add(CommentResDto.builder()
                    .id(comment.getId())
                    .commenter(comment.getMember().getEmail())
                    .content(comment.getContent())
                    .modifiedAt(comment.getModifiedAt())
                    .build()
            );
        }
        
        return PostResponseDto.builder()
        .id(post.getId())
        .title(post.getTitle())
        .content(post.getContent())
        .email(post.getMember().getEmail())
        .modifiedAt(post.getModifiedAt())
        .comments(commentList)
        .build();
    }
```

⬇️


```java
    // 게시글 상세 조회
    @Transactional(readOnly = true)
    public PostResponseDto getOnePost(Long id) {
        Post post = validateCheck.getPostIfExists(id);


        // 게시글 상세 조회 시 댓글도 함께 조회
       List<CommentResDto> commentResDtos = commentRepository.findByPostId(id)
            .stream()
            .map(comment -> CommentResDto.builder()
                    .id(comment.getId())
                    .commenter(comment.getMember().getEmail())
                    .content(comment.getContent())
                    .modifiedAt(comment.getModifiedAt())
                    .build())
            .toList();

        
        return PostResponseDto.builder()
        .id(post.getId())
        .title(post.getTitle())
        .content(post.getContent())
        .email(post.getMember().getEmail())
        .modifiedAt(post.getModifiedAt())
        .comments(commentList)
        .build();
    }
```

<br/>
<br/>
