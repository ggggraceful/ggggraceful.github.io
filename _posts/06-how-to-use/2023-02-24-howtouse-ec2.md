---
title: 🔍 AWS EC2 인스턴스 생성, ubuntu 접속 
author: ggggraceful
date: 2023-02-24
categories: [06.HOW TO USE]
tags: [how to use]
---

<br/>
<br/>

# EC2 인스턴스 생성

---

<br/>

![](https://velog.velcdn.com/images/ggggraceful/post/83ab6610-c896-445e-81ef-a3c010c40eed/image.png)

우툰투 + 프리티어 사용가능 한 것 선택

<br/>
<br/>

이미 가지고 있는 키페어를 사용할 것이라면 해당 키페어 선택

새로 만들거라면
RSA 유형으로 선택후 생성하고, 다운받아 원하는 폴더 안에 넣어주기

![](https://velog.velcdn.com/images/ggggraceful/post/edc97fab-45da-4967-874a-55d573400f23/image.png)

다른것은 만지지말고 생성완료!

<br/>
<br/>

![](https://velog.velcdn.com/images/ggggraceful/post/8891ef80-17f3-4482-94f9-cb74560d37d5/image.png)


> - 인스턴스 시작: 우분투 컴퓨터 실행  
> - 인스턴스 중지: 우분투 컴퓨터 중지  
> - 인스턴스 종료: 우분투 컴퓨터 삭제  
> <br/>  
> 인스턴스를 종료하면 새로 인스턴스를 생성해야함  
> 또 종료후 다시 실행한다면 ip주소가 바뀜

<br/>
<br/>
<br/>

# 인스턴스 인바운드 규칙

---

<br/>

'인스턴스 ID' 클릭

![](https://velog.velcdn.com/images/ggggraceful/post/42769a15-7343-483a-9304-2376024e3f52/image.png)

<br/>
<br/>

아래 '보안' 클릭


![](https://velog.velcdn.com/images/ggggraceful/post/2dd48ed0-840c-4fba-be78-6b0fa75c04f2/image.png)

<br/>
<br/>

'보안 그룹' 클릭

![](https://velog.velcdn.com/images/ggggraceful/post/74b19461-cbc7-4e38-8959-ed0f0a9d8c6d/image.png)

<br/>
<br/>

'인바운드 규칙 편집' 클릭

![](https://velog.velcdn.com/images/ggggraceful/post/40af46c6-d292-4651-b49d-95b8cc49b609/image.png)

<br/>
<br/>

다음과같이 인바운드 규칙 편집 후 '규칙저장'

![image](https://github.com/ggggraceful/ggggraceful/assets/109974940/637e44e6-3efd-4103-88f3-5ce69178e932)

이 설정은 내 아이피에서만 접속 가능하게 하는 것이고,  
다른 팀원들의 아이피도 추가하게 된다면 이 서버에 접속 가능하게 될 것이다.  

<br/>
<br/>
<br/>

# 권한 부여

---

(최초 1번)

<br/>

터미널에 들어가 다음을 입력후 엔터

```
chmod 400 [키페어 파일 드래그해서 위치와 함께 불러오기]
```

![](https://velog.velcdn.com/images/ggggraceful/post/5d97a3b7-e69e-4f82-946e-e2d3e14940f6/image.png)



<br/>

|8진수|권한|
|----|---|
|400|	파일 소유자의 읽기 권한|
|200|	파일 소유자의 쓰기 권한|
|100|	파일 소유자의 실행 권한|
|40	|그룹 사용자의 읽기 권한|
|20	|그룹 사용자의 쓰기 권한|
|10	|그룹 사용자의 실행 권한|
|4	|다른 모든 사용자의 읽기 권한|
|2	|다른 모든 사용자의 쓰기 권한|
|1	|다른 모든 사용자의 실행 권한|

<br/>

{: .prompt-info }
> 연산자
> + : 권한 부여
> - : 권한 해제

<br/>

{: .prompt-info }
> 접근권한  
> 읽기(read) : r  
> 쓰기(write) : w  
> 실행(excute) : e  

<br/>
<br/>
<br/>

# ubuntu 컴퓨터로 원격 접속

---

(ec2의 인스턴스가 실행중인 상태에서 진행)

<br/>

다음을 넣어주면 우분투 컴퓨터에 접속할 수 있다.

```
ssh -i [키페어파일 경로] ubuntu@[ec2 퍼블릭 IPv4 주소]
```

![](https://velog.velcdn.com/images/ggggraceful/post/673039ca-0a9d-439c-9e41-146b6b9b8da9/image.png)


<br/>
<br/>

ec2 퍼블릭 IPv4 주소는

실행중인 인스턴스ID를 누르고

![](https://velog.velcdn.com/images/ggggraceful/post/935e8aac-8661-4339-9daa-c478584da1ff/image.png)

<br/>
<br/>

퍼블릭 IPv4 주소를 복사해 해당 부분에 넣어주면 된다.

![image](https://github.com/ggggraceful/ggggraceful/assets/109974940/4a78f761-0005-47e6-b432-562bf6acf760)


<br/>
<br/>

계속해서 연결할 거니
```
yes
```

<br/>
<br/>


우분투 컴퓨터에 접속 완료!

![](https://velog.velcdn.com/images/ggggraceful/post/f6bcdc86-c408-463c-b62d-f30b95af7a9e/image.png)



