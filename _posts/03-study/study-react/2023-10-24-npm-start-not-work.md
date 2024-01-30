---
title: npm start 작동하지 않는 문제
author: ggggraceful
date: 2023-10-24
categories: [03.STUDY, react]
tags: [study, react]
---

<br/>
<br/>

공부용으로 만들어 놓은 리액트 프로젝트를  
.zip 으로 만들어 다른 컴퓨터로 가지고 와 실행을 하려는데  
"npm start" 가 작동하지 않았다.  


리액트 기본적으로 셋팅하고 실행할 때에는 이 정도 사용하였다.   
~~~
> npm install
> npm start
~~~


![스크린샷 2023-10-24 오후 11 40 39](https://github.com/ggggraceful/ggggraceful/assets/109974940/4a97e3a1-65cc-4a5a-ae07-9d748f5ea9ad)
하지만 다음과 같이  

"Permission denied" 가 떴다.  


<br/>
<br/>


일단 내가 선택한 방법은  

node_modules 와
package-lock.json 파일을 제거하고  

다시 npm install 을 하는 방법이다.  



저 파일들안에 처음 프로젝트를 생성할 때 권한이 들어갔었는지  
새로운 환경에서 실행시킬경우 권한에 관한 오류를 마주했다.   

해당 파일들을 삭제하고 재설치 했을 때 다시 셋팅이 되어  
더이상 권한 관련한 문제는 발생하지 않았다.  

<br/>
<br/>

이어서 연습중이었던 리액트 프로젝트를 완성시키러 가본다.


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
