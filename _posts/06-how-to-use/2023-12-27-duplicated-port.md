---
title: 🔍 포트 죽이기
author: ggggraceful
date: 2023-12-27
categories: [03.STUDY, etc]
tags: [STUDY]
---

<br/>
<br/>

프로젝트를 실행하면 가끔 이미 해당 포트가 실행중이어서 사용이 불가하다는 메세지가 나오곤한다.  
프로세스를 종료하게 되면 해당 PID삭제와 함께 이루어져야하는데  
프로세스는 종료한 것처럼 보이지만, PID가 살아있는 경우 종종 이런 메세지를 볼 수 있다.  

이 경우에는 해당 포트의 PID를 찾고 kill 명령어를 사용하면 된다.  

<br/>
<br/>

# 터미널 입력  

---

1. 해당 포트를 이미 사용하고 있는 PID 찾기

```
lsof -n -i TCP:포트번호
또는
lsof -i 포트번호
```

<br/>
<br/>

2. 포트번호로 찾은 PID로 포트를 강제 종료 한다.

```
kill -9 00000  
>> 00000: PID 숫자
```

<br/>
<br/>

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

