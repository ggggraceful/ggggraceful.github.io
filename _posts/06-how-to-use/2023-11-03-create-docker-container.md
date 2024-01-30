---
title: 🔍 Docker container 애서 MySQL 사용하기
author: ggggraceful
date: 2023-11-03
categories: [06.HOW TO USE]
tags: [how to use]
---

# 1. mysql 이미지 불러오기
```
sudo docker pull mysql
```

# 2. 도커 이미지 확인
```
sudo docker images
```

# 3. 도커 컨테이너 생성
```
sudo docker run -d -p 3305:3306 -e MYSQL_ROOT_PASSWORD=mypassword --restart=unless-stopped -v /home/ubuntu/db:/var/lib/mysql --name mymysqldb mysql
```

- -d  : detached모드로 컨테이너 실행, 컨테이너를 백그라운드에서 동작하는 애플리케이션으로써 실행하도록 설정

- -p 3305:3306  : 컨테이너의 포트를 호스트의 포트와 바인딩
                     호스트의 3305번 포트를 컨테이너의 3306번 포트와 연결하겠다


- -v /home/ubuntu/db:/var/lib/mysql  : 호스트와 볼륨을 공유
호스트의 /home/ubuntu/db폴더와  컨테이너의 /var/lib/mysql폴더를 동기화(연결)하겠다

- -e  : 컨테이너에서 사용할 환경변수 설정

- MYSQL_ROOT_PASSWORD=1234  : mysql root 비밀번호를 1234로 지정하겠다

- --name test_mysql  : 컨테이너의 이름을 test_mysql로 지정하겠다

- --restart=  : 컨테이너 내부의 프로세스 종료시 재시작 정책 설정

- unless-stopped  : 부팅시 자동으로 컨테이너를 재시작 하겠다



---

(참고)

- [도커를 사용해서 MYSQL설치하고 접속하기](https://dev-taerin.tistory.com/13)

