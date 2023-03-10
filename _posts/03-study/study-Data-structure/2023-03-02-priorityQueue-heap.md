---
title: /Data structure/ ๐ฌ Priority Queue, Heap
author: ggggraceful
date: 2023-03-02
categories: [03.STUDY, Data structure]
tags: [STUDY]
---

<br/>
<br/>

{: .prompt-tip }
> โ๏ธ ํ(Queue)    
> : ๋จผ์  ๋ค์ด์ค๋ ๋ฐ์ดํฐ๊ฐ ๋จผ์  ๋๊ฐ๋ FIFO(First In First Out) ํ์์ ์๋ฃ๊ตฌ์กฐ  
> โ๏ธ ์ฐ์ ์์ ํ(Priority Queue)  
> : ๋จผ์  ๋ค์ด์ค๋ ๋ฐ์ดํฐ๊ฐ ์๋๋ผ, ์ฐ์ ์์๊ฐ ๋์ ๋ฐ์ดํฐ๊ฐ ๋จผ์  ๋๊ฐ๋ ํํ์ ์๋ฃ๊ตฌ์กฐ,  
>   ์ฐ์ ์์ ํ๋ ์ผ๋ฐ์ ์ผ๋ก ํ(Heap)์ ์ด์ฉํ์ฌ ๊ตฌํ,   
>   ๋ฐฐ์ด๊ณผ ์ฐ๊ฒฐ๋ฆฌ์คํธ๋ฅผ ์ด์ฉํด์๋ ๊ตฌํ๊ฐ๋ฅ

<br/>
<br/>

# ํ(Heap)

---

- ํ(Heap)์ ์ฐ์ ์์ ํ๋ฅผ ์ํด ๊ณ ์๋ `์์ ์ด์งํธ๋ฆฌ` ํํ์ ์๋ฃ๊ตฌ์กฐ  
  - [์ด ๋ธ๋ก๊ทธ์ ๋ค๋ฅธ๊ธ- ํธ๋ฆฌ](https://ggggraceful.github.io/posts/tree/)
- ์ฌ๋ฌ ๊ฐ์ ๊ฐ ์ค ์ต๋๊ฐ ๋๋ ์ต์๊ฐ์ ์ฐพ์๋ด๋ ์ฐ์ฐ์ด ๋น ๋ฆ

<br/>
<br/>

# ํ์ ํน์ง

---

<br/>

- ์์ ์ด์งํธ๋ฆฌ ํํ๋ก ์ด๋ฃจ์ด์ง
- ๋ถ๋ชจ๋ธ๋์ ์๋ธํธ๋ฆฌ๊ฐ ๋์ ๊ด๊ณ๊ฐ ์ฑ๋ฆฝ๋จ (๋ฐ์ ๋ ฌ ์ํ)
- ์ด์งํ์ํธ๋ฆฌ(BST)์ ๋ฌ๋ฆฌ ์ค๋ณต๋ ๊ฐ์ด ํ์ฉ

<br/>
<br/>

# ํ์ ์ข๋ฅ

---

<br/>

- ์ต๋ ํ (Max Heap)  
: ๋ถ๋ชจ ๋ธ๋์ ํค ๊ฐ์ด ์์ ๋ธ๋๋ณด๋ค ํฌ๊ฑฐ๋ ๊ฐ์ ์์ ์ด์งํธ๋ฆฌ  
  key(๋ถ๋ชจ๋ธ๋) โฅ key(์์๋ธ๋)  

<br/>

![แแณแแณแแตแซแแฃแบ 2023-03-02 แแฉแแฎ 3 52 49](https://user-images.githubusercontent.com/109974940/222353139-0dd0e555-10dc-4c8c-ac45-569fd5ee09d1.png)

<br/>

- ์ต์ ํ (Min Heap)  
: ๋ถ๋ชจ ๋ธ๋์ ํค ๊ฐ์ด ์์ ๋ธ๋๋ณด๋ค ์๊ฑฐ๋ ๊ฐ์ ์์ ์ด์งํธ๋ฆฌ  
  key(๋ถ๋ชจ๋ธ๋) โฅ key(์์๋ธ๋) 

<br/>

![แแณแแณแแตแซแแฃแบ 2023-03-02 แแฉแแฎ 3 53 07](https://user-images.githubusercontent.com/109974940/222353193-82667357-01e0-4aa8-b218-4bbd0a72c169.png)

<br/>

# ์ ์์ ํ ๊ตฌํ๋ฐฉ๋ฒ ๋น๊ต

---

- ๋ฐฐ์ด๊ณผ ์ฐ๊ฒฐ๋ฆฌ์คํธ
  - ์ ํ ๊ตฌ์กฐ์ ์๋ฃ๊ตฌ์กฐ
  - ์ฝ์ ๋๋ ์ญ์  ์ฐ์ฐ์ ์ํ ์๊ฐ๋ณต์ก๋๋ O(n)

- ํํธ๋ฆฌ
  - ์์ ์ด์งํธ๋ฆฌ ๊ตฌ์กฐ
  - ํํธ๋ฆฌ์ ๋์ด๋ logโ(n+1)
  - ํ์ ์๊ฐ๋ณต์ก๋๋ O(logโn)


| ๊ตฌํ๋ฐฉ๋ฒ       | ์ฝ์       | ์ญ์   |
|------------|----------|-----|
| ์์์๋ ๋ฐฐ์ด    | O(1)     |  O(n)   |
| ์์์๋ ์ฐ๊ฒฐ๋ฆฌ์คํธ | O(1)     | O(n)    |
| ์ ๋ ฌ๋ ๋ฐฐ์ด     | O(n)     |  O(1)     |
| ์ ๋ ฌ๋ ์ฐ๊ฒฐ๋ฆฌ์คํธ  | O(n)     |   O(1)    |
| ํ          | O(logโn) | O(logโn) |


# ์ฐ์ ์์ ํ ADT

---

<br/>




<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

---

(์ฐธ๊ณ )

- [์ฐ์ ์์ ํ์ ํ (Priority Queue & Heap)](https://suyeon96.tistory.com/31)
- 

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> ๊ณต๋ถํ ๋ด์ฉ์ ์ฌ๋ฌ๊ธ๊ณผ ์ฑ ์ฝ์ ๋ด์ฉ์ ๋ฐํ์ผ๋ก ์ ๋ฆฌํ๊ณ  ์์ต๋๋ค.</span>  
<span style="font-size: 12px; color:  #cbce91"> ์ข์ ๊ธ๋ก ์ ์ ๊ณต๋ถ์ ๋์์ ์ฃผ์๋ ๋ถ๋ค๊ป ๊ฐ์ฌ๋๋ฆฝ๋๋ค. </span>

<!--

โค๏ธ๋ฉด์ ์์์ง๋ฌธ โค๏ธ

-->

