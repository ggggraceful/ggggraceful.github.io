---
title: /Database/ HTTP, HTTPS
author: ggggraceful
date: 2023-01-16
categories: [03.STUDY, Database]
tags: [study, database]
---

<br/>
<br/>

## 📌 HTTP

---

HyperText Transfer Protocol

- 인터넷 상에서 클라이언트와 서버가 자원을 주고 받을 때 쓰는 통신 규약
- 서버/클라이언트 모델을 따라 데이터를 주고 받기 위한 프로토콜 (80번 포트를 사용)  
- 인터넷을 작동시키는 역할을 하며,   
  웹 서버 및 웹 브라우저 상호 간의 데이터 전송을 위한 응용계층 ```프로토콜```입니다.

<br/>

{: .prompt-info }
✔️프로토콜  
-컴퓨터 내부에서, 또는 컴퓨터 사이에서  
　데이터의 교환 방식을 정의하는 규칙 체계  
-기기 간 통신은 교환되는 데이터의 형식에 대해 상호 합의를 요구함

<br/>

- HTTP는 암호화가 되지 않은 평문 데이터를 전송하는 프로토콜이였기 때문에,
- HTTP로 비밀번호나 주민등록번호 등을 주고 받으면 제3자가 정보를 조회할 수 있었다.

➡️ 그리고 이러한 문제를 해결하기 위해 HTTPS가 등장하게 되었다.

<br/>
<br/>

### HTTP 1 / HTTP 2

---

HTTP1은 기본적으로 연결당 하나의 요청/응답을 처리하여 다음과 같은 문제를 가지고 있었다.

- HOL(Head Of Line) Blocking (특정 응답 지연)  
  :클라이언트의 요청과 서버의 응답이 동기화되어 지연 발생
- RTT(Round Trip TIme) 증가 (양방향 지연)  
  :패킷 왕복 시간의 지연 발생
- 헤더 크기의 비대  
  :쿠키 등과 같은 메타데이터에 의해 헤더가 비대해짐

<br/>

그리고 HTTP2는 다음과 같은 기술을 사용하여 HTTP1의 성능 문제를 해결하였다.

- Multiplexed Streams  
  :하나의 커넥션으로 여러 개의 메세지를 동시에 주고 받을 수 있음
- Stream Prioritization  
  :요청온 리소스간의 의존관계를 설정하여 먼저 응답해야하는 리소스를 우선적으로 반환함
- Header Compression  
  :헤더 정보를 HPACK 압축 방식을 이용하여 압축 전송함
- Server Push  
  :HTML문서 상에 필요한 리소스를 클라이언트 요청없이 보내줄 수 있음

<br/>

![사진](https://user-images.githubusercontent.com/109974940/213090427-851d410c-bacf-48a6-813e-8261bb0a61be.png)

<br/>
<br/>

### HTTP의 구조

---

- 애플리케이션 레벨의 프로토콜로 TCP/IP 위에서 작동한다. 
- 상태를 가지고 있지 않는 Stateless 프로토콜이다.
- Method, Path, Version, Headers, Body 등으로 구성된다.

<br/>

![http 구조](https://user-images.githubusercontent.com/109974940/213016368-06f17ac8-5dbe-4155-bace-ee0cf4469943.png)

<br/>

![구조](https://user-images.githubusercontent.com/109974940/213091210-f1895355-9c8b-4d9b-9fcd-16bbc00fab0e.png)

<br/>

- 시작 줄(start-line)  
  :HTTP 요청 / 또는 요청에 대한 성공 또는 실패가 기록된다. 항상 한 줄로 끝난다.
- HTTP 헤더  
  :시작 줄 다음으로 요청에 대한 설명 / 또는 메시지 본문에 대한 설명이 들어간다.
- 빈 줄  
  :요청에 대한 모든 메타 정보가 전송되었음을 알리는 빈 줄이 삽입된다. (헤드와 본문 사이)
- 본문(optional)  
  :요청과 관련된 데이터(HTML form 콘텐츠 등) / 또는 응답과 관련된 문서(document)가 선택적으로 들어간다.  
   본문의 존재와 크기는 시작 줄 및 HTTP 헤더에 명시된다.  

HTTP 메시지의 시작 줄과 HTTP 헤더를 묶어서 요청 헤드(head) 라고 부르며,  
이와 반대로 HTTP 메시지의 페이로드는 본문(body) 이라고 한다.

<br/>
<br/>


## 📌 HTTPS

---

Hypertext Transfer Protocol Secure  
(HyperText Transfer Protocol over Secure Socket Layer, HTTP over TLS, HTTP over SSL, HTTP Secure 등)

- HTTP에 데이터 암호화가 추가된 프로토콜 (443번 포트를 사용)
- 인터넷 상에서 정보를 암호화하는 SSL 프로토콜을 사용해 클라이언트와 서버가 자원을 주고 받을 때 쓰는 통신 규약

<br/>

- 표준 HTTP와 동일한 방식으로 작동하지만,  
  서버와 주고받는 데이터가 암호화되기 때문에 웹사이트에 추가적인 보호를 제공한다.
- 개인 데이터를 훔치거나, 해킹하거나 볼 수 없도록 작동한다.
- 네트워크 상에서 중간에 제3자가 정보를 볼 수 없도록 암호화를 지원하고 있다.

<br/>

{: .prompt-info }
✔️HTTPS 확인 방법  
-브라우저에서 URL을 확인하여 웹사이트에 HTTPS 보호 기능이 있는지를 확인할 수 있음  
-도메인 이름 앞에 자물쇠 아이콘이 있으면 당신의 사이트는 HTTPS로 인해 안전한 것

<br/>
<br/>

## 📌 HTTPS가 더 안전한 원리

---

- ```SSL/TLS``` 프로토콜을 사용하여 
  공격자가 데이터를 도용할 수 없도록 통신을 암호화 해준다.
- 웹사이트 서버가 누구인지 확인하여  
  명의 도용을 방지해주어 더 안전하게 사용할 수 있게 해준다.  

<br/>
<br/>

### SSL/TLS(Secure Sockets Layer)  

---

SSL(Secure Socket Layer)  
TLS(Transport Layer Security)

- 암호화 기반 인터넷 보안 프로토콜
- 안전한 계층(layer)을 웹 통신에 추가하는 방식
- TLS는 SSL의 개선 버전으로,  
  최신 인증서는 대부분 TLS를 사용하지만, 편의적으로 SSL 인증서라고 말한다.
- 이 기술을 수행하기 위해 웹 서버에 설치하는 것이 SSL/TLS 인증서이다.
- 웹 브라우저는 공신력 있는 인증서의 정보를 브라우저 내부에 보관하고 있으며,  
  접속하는 웹 사이트에 믿을만한 인증서가 설치되어 있는지 확인한다.


<br/>
<br/>

## 📌 HTTPS 연결 과정

---

HTTP는 평문 데이터를 전송하는 프로토콜이기 때문에, HTTP로 비밀번호나 주민번호 등을 주고 받으면 제3자에 의해 조회될 수 있습니다. 이러한 문제를 해결하기 위해 HTTP에 암호화가 추가된 프로토콜이 HTTPS입니다.   

 HTTPS에는 대칭키 암호화와 비대칭키 암호화가 모두 사용됩니다. 비대칭키 암/복호화는 비용이 매우 크기 때문에 서버와 클라이언트가 주고받는 모든 메세지를 비대칭키로 암호화하면 오버헤드가 발생할 수 있습니다. 그래서 서버와 클라이언트가 최초 1회로 서로 대칭키를 공유하기 위한 과정에서 비대칭키 암호화를 사용하고, 이후에 메세지를 주고 받을 때에는 대칭키 암호화를 사용합니다. 이러한 과정을 정리하면 다음과 같습니다.

1. 클라이언트(브라우저)가 서버로 최초 연결 시도를 함
2. 서버는 공개키(엄밀히는 인증서)를 브라우저에게 넘겨줌
3. 브라우저는 인증서의 유효성을 검사하고 세션키를 발급함
4. 브라우저는 세션키를 보관하며 추가로 서버의 공개키로 세션키를 암호화하여 서버로 전송함
5. 서버는 개인키로 암호화된 세션키를 복호화하여 세션키를 얻음
6. 클라이언트와 서버는 동일한 세션키를 공유하므로 데이터를 전달할 때 세션키로 암호화/복호화를 진행함

<br/>
<br/>

## 📌 HTTP를 사용하면 무조건 안전한가?

---

HTTPS도 무조건 안전한 것은 아니다.  
(신뢰받는 CA 기업이 아닌 자체 인증서 발급한 경우 등)  
이때는 HTTPS지만 브라우저에서 주의 요함, 안전하지 않은 사이트와 같은 알림으로 주의 받게 된다.  

HTTPS는 웹에서 보안을 적용하기 위한 가장 기본적인 단계이고, 이것으로 모든 보안성이 완벽하게 지켜졌다고 할 순 없다.

 예를 들면, 웹 서버가 해커의 다양한 공격에 의해 루트 권한을 탈취당했다면, 모든 기밀 데이터를 열람할 수 있는 권한이 넘어갈 수도 있다. 또한 HTTPS는 전달 구간에 대한 보안 기술인데, 전달 구간 중간에 해커가 중간자 공격을 수행할 수 있는 취약점이 있다면 HTTPS는 유지되지만 전달하는 내용은 고스란히 노출되기 때문이다.

따라서 인스턴트 메시징 서비스와 같이 개인 간 혹은 그룹 간 대화, 민감한 개인 정보 등의 전달에서는 HTTPS를 적용하면서도, 종단 간 암호화 기술을 추가로 적용하여 HTTPS가 무력화되어도 노출된 데이터는 암호화를 유지해, 외부로 노출되지 않도록 하는 방법이 일반적으로 쓰인다.

<br/>
<br/>

---

(참고)  

- [[Web] HTTP와 HTTPS의 개념 및 차이점](https://mangkyu.tistory.com/98)
- [HTTP HTTPS 차이: 당신의 웹 사이트는 안전한가요?](https://www.ascentkorea.com/difference-between-http-and-https/)
- [HTTP & HTTPS](https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Network/HTTP%20%26%20HTTPS.md)
- [Http와 Https 이해와 차이점 그리고 오해(?)](https://jeong-pro.tistory.com/89)
- [안전한 웹을 위해 HTTPS 이해하기: ①HTTPS의 작동 원리,요즘IT](https://yozm.wishket.com/magazine/detail/1852/)
- [7계층 HTTP 프로토콜](https://the-cloud.tistory.com/36)
- [네트워크/HTTP 모의면접 질문 리스트](https://juicyjerry.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%ACHTTP-%EB%AA%A8%EC%9D%98%EB%A9%B4%EC%A0%91-%EC%A7%88%EB%AC%B8-%EB%A6%AC%EC%8A%A4%ED%8A%B8)
- [HTTPS와 HTTP의 차이점. 핵심은 SSL/TLS [ 네트워크 면접질문 6 ]](https://murphymoon.tistory.com/m/entry/HTTPS%EC%99%80-HTTP%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90-%ED%95%B5%EC%8B%AC%EC%9D%80-SSLTLS-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EB%A9%B4%EC%A0%91%EC%A7%88%EB%AC%B8-6)
- [[기술면접] CS 기술면접 질문 - 네트워크 (4/8)](https://mangkyu.tistory.com/91)
- [](https://velog.io/@bky373/Web-HTTP%EC%99%80-HTTPS-%EC%B4%88%EA%B0%84%EB%8B%A8-%EC%A0%95%EB%A6%AC)
- [HTTP](https://developer.mozilla.org/ko/docs/Web/HTTP/Messages)

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>

<!--

❤️면접예상질문 ❤️

-->
