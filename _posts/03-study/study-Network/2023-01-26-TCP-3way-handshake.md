---
title: /Network/ TCP 3 way handshake
author: ggggraceful
date: 2023-01-26
categories: [03.STUDY, Network]
tags: [STUDY]
---

<br/>
<br/>

# TCP 3 way handshake

---

- TCP/IP 네트워크 환경에서 서버와 클라이언트를 연결하는데 필요한 프로세스

- TCP/IP프로토콜을 이용해서 통신을 하는 응용프로그램이  
  데이터를 전송하기 전에 먼저 정확한 전송을 보장하기 위해  
  상대방 컴퓨터와 사전에 세션을 수립하는 과정
  (= 전송 제어 프로토콜(TCP)에서   
   통신을 하는 장치간 서로 연결이 잘 되어있는지 확인하는 과정, 방법)


# TCP 3 way handshake 과정

---

데이터를 주고받기 전에 서버와 클라이언트가 확인 패킷을 3단계로 교환하여 연결을 맺는다.

<br/>

![스크린샷](https://user-images.githubusercontent.com/109974940/214766458-81bd91fd-5ee0-4fcf-9e74-e3f1515b0249.png)

<br/>

1) 클라이언트에서  
　　서버에 SYN 패킷을 보내고   
　　( 클라이언트 상태 : SYN_SENT로 변경 )  

2) 서버는   
　　클라이언트로부터 SYN를 받고  
　　응답 패킷 ACK과 SYN 패킷을 보냄  
　　( 서버 상태 : LISTEN ➡️ SYS-SENT로 변경 )  

3) 클라이언트는   
　　받은 패킷에 대한 응답으로 ACK 패킷을 서버로 보냄  
　　( 클라이언트 상태 : ESTABLISHED )  
　　( 서버 상태 : ESTABLISHED로 변경 )  

➡️ 위 과정을 통해 서버와 클라이언트는 신뢰된 연결을 맺게 됩니다.

<br/>

{: .prompt-tip }
> LISTEN 	: 포트가 열려있어서 연결을 기다리고 있는 상태
> SYS-SENT	: 연결 요청한 상태(SYN 보냄)
> SYN_RECEIVED	: 요청을 받아서(SYN) 응답한 상태(SYN+ACK), 그러나 아직 ACK는 받지 못한 상태임
> ESTABLISHED	: 연결된 상태

## TCP FLAG

---

- SYN: 연결 요청 플래그
- ACK: 응답플래그
- FIN: 연결종료 플래그
- RST: 연결 재설정 플래그
- PSH: 밀어넣기
- URG: 긴급 데이터 플래그

<br/>
<br/>

## 3-way Handshake 확인 

---

<br/>

### 1. tcpdump로 3-way Handshake 확인

---

test-1 서버(출발지)에서  
목적지 KT DNS 서버(168.126.63.1) 53 포트 telnet 접속을  
tcpdump로 덤프를 뜬 내용이다.  
  
tcpdump에서는 ACK 플래그를 "."(점)으로 표시합니다.  

<br/>
  
<span style="color:blue">test-1</span> ➡️ <span style="color:red">서버</span> : **S**  
<span style="color:red">서버</span> ➡️ <span style="color:blue">test-1</span> : **S.**  
<span style="color:blue">test-1</span> ➡️ <span style="color:red">서버</span> : **.**  

<br/>

![스크린샷](https://user-images.githubusercontent.com/109974940/214987900-d6276289-90b2-48b1-8b27-4833321213c2.png)

<br/>
<br/>

### 2. wireshark로 3-way Handshake 확인

---

192.168.210.102(출발지)에서   
목적지 KT DNS 서버(168.126.63.1) 53 포트 telnet 접속을   
wireshark로 덤프를 뜬 내용이다.

<br/>

<span style="color:blue">클라이언트</span> ➡️ <span style="color:red">서버</span> : **SYN**  
<span style="color:red">서버</span> ➡️ <span style="color:blue">클라이언트</span> : **SYN, ACK**   
<span style="color:blue">클라이언트</span> ➡️ <span style="color:red">서버</span> : **ACK**  

<br/>

![스크린샷](https://user-images.githubusercontent.com/109974940/214989660-2daea49a-0528-43f2-95b5-31a9d820ecf2.png)

<br/>
<br/>

---

(참고)

- [..](https://mindnet.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-22%ED%8E%B8-TCP-3-WayHandshake-4-WayHandshake
  )
- [[TCP] 3-way Handshake란? / 와이어샤크, tcpdump 확인](https://sh-safer.tistory.com/142)
- [[TCP] 4-way Handshake란? / 와이어샤크, tcpdump 확인](https://sh-safer.tistory.com/146)

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>

<!--

❤️면접예상질문 ❤️

-->
