---
title: 🔍 Git 여러개의 commit 1개로 합치기 
author: ggggraceful
date: 2024-02-21
categories: [06.HOW TO USE]
tags: [how to use]
---

<br/>
<br/>

요즘 유용하게 사용하고 있는 커밋 합치기에 대해 공유해보려한다.
커밋을 여러번 했지만 한개로 합치고 싶을 때 이 방법을 사용하면 깔끔한 히스토리를 가질 수 있다.


1. 해당 브랜치로 체크아웃
---
```
git checkout [BRANCH-NAME]
```
먼저 해당 브랜치로 체크아웃을 해준다.  
리베이스 중이거나 하면 동작하지 않으니, 리베이스를 중단하고 깔끔하게 체크아웃해주어야한다.  

<br/>
<br/>

2. 합치고 싶은 커밋으로 rebase
---

```
git rebase -i HEAD~[숫자]
```

![스크린샷 2024-02-22 오후 9 48 38](https://github.com/ggggraceful/ggggraceful/assets/109974940/124115e3-44e2-456a-a546-51becc7abe1b)

그 커밋이 가장 최근 커밋으로 부터 3번째라면  

```
git rebase -i HEAD~3
```
해주면 된다. 


하지만 프로젝트의 맨 첫번째  커밋에는 안된다;
2번째 커밋과 3번째 커밋을 합쳐보겠다.



2. 합칠 커밋중 가장 과거의 커밋에 합쳐준다. 
---

![스크린샷 2024-02-22 오후 10 04 16](https://github.com/ggggraceful/ggggraceful/assets/109974940/6b9c098a-5947-4bc9-915b-645ff56b78a3)

이러한 화면이 나오고 
오름차순으로 나열되어 맨위에 있는 커밋이 가장 오래된 커밋이다.



![스크린샷 2024-02-22 오후 10 06 30](https://github.com/ggggraceful/ggggraceful/assets/109974940/c8e13d7c-3108-4a75-9032-ef1921468775)

합칠 커밋을 그대로 pick 으로 두고
그 pick한 커밋에 넣어줄 커밋을 pick 대신 s 로 넣어주면된다.
작성은 i를 눌러 아래 insert 표시가 되었을 때 수정해주고  



![스크린샷 2024-02-22 오후 10 07 13](https://github.com/ggggraceful/ggggraceful/assets/109974940/f6d1a39b-1267-4613-bba4-b7878c08dfda)

저장은 esc 눌러주고, :wq 적어주고 엔터누르면 된다.  



3. 대표로 사용할 커밋메세지 하나를 선택하고, 나머지는 주석처리 해준다. 

---

![스크린샷 2024-02-22 오후 10 13 58](https://github.com/ggggraceful/ggggraceful/assets/109974940/a068904a-9e57-478f-9ee0-5e3a7f29f72d)

대표로 사용한 커밋메세지 하나만 남겨두고  
다른 커밋메시지는 앞에 #을 붙여 주석처리해준다. 

방금과 같은 방법으로  
작성은 i를 눌러 아래 insert 표시가 되었을 때 수정해주고  
저장은 esc 눌러주고, :wq 적어주고 엔터누르면 된다.



4. 로컬 커밋 합치기 완료  

---

![스크린샷 2024-02-22 오후 10 16 00](https://github.com/ggggraceful/ggggraceful/assets/109974940/41ee7b8d-1fa3-4114-bdab-5516d252982e)


5. 원격 커밋 합치기

---

~~~

~~~



이제 원격으로 푸쉬




---

(참고)

- [..](..)

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>

<!--

❤️면접예상질문 ❤️

-->

