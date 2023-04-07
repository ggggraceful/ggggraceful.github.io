---
title: /etc/ Docker 기초 이론
author: ggggraceful
date: 2023-04-05
categories: [03.STUDY, etc]
tags: [STUDY]
---

<br/>
<br/>

서버운영에서 인프라 관리와 application 작성을 분리하고,  
application 실행에 필요한 모든 파일을 Docker image에 담아둔다.

실행환경 세팅, 실행하는 코드, 필요한 라이브러리 설정파일들을 직접 세팅하는 것이 아니고,  
Docker image를 받은 다음 실행하는 구조

이 image를 실행하는 것을 container라고 한다.

![사진](https://user-images.githubusercontent.com/109974940/230051716-c8f95cc3-edfc-4248-ac3b-775c20c87457.png)

Docker Registry
Docker image를 쉽게 공유하기 위해서 Docker Registry를 사용한다.
Registry에 image를 등록하고,  
Registry로부터 image를 다운받는 방식으로 사용  

Docker Daemon
image를 Registry로부터 다운받거나 올리기  
image로부터 container 실행
imgage를 새로 만드는 등의
진짜 Docker object(image, container 등)들, 볼륨, 네트워크 등을 관리하는 주체

Docker Cli 
client에서 Docker Daemon으로 명령  
docker build(도커 이미지 생성),  
docker pull(도커 이미지를 registry에서 다운), 
docker run(이미 있는 이미지로 부터 container를 생성)

<br/>
<br/>

# Docker와 가상 머신(VM)의 차이

---

<br/>

![..](https://user-images.githubusercontent.com/109974940/230052156-e94d5946-bb1f-4022-a407-5f5acb9d2624.png)

왼쪽이 VM, 오른쪽이 Docker

## VM

VM서버에서 OS를 설치  
➡️ HyperVisor 프로그램 설치  
스➡️ Binary, 필요한 실행 파일, Library를 다운
➡️ application 코드를 받아서 실행

- 여러개의 application을 실행하려고 하면  
  여러개의 OS를 생성해야함

## Docker

Host OS에서 Docker Engine을 통해  
직접 OS를 다운 받지 않고  
Binary, Library를 다운받아  
바로 application을 실행

도커가 프로세스별 리소스(디스크, 네트워크 등)를 분리해  
각각의 독립성을 보장할 수 있게 함


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
