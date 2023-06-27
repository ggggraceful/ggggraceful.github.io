---
title: /Database/💬 MySQl/Mysql 엔진 아키텍쳐
author: ggggraceful
date: 2023-03-17
categories: [03.STUDY, Database]
tags: [study, database]
---

<br/>
<br/>

{: .prompt-tip }
> ✔️ MySQL 서버  
> - MySQL 엔진 : 사람의 머리 역할을 담당  
> 　　- InnoDB 스토리지 엔진    
> 　　- MyISAM 스토리지 엔진  
> - 스토리지 엔진 : 손발 역할을 담당  
> 　　- 핸들러 API를 만족하면 누구든 스토리지 엔진을 구현해서 MySQL 서버에 추가해서 사용 가능 
  
<br/>
<br/>

# 1 MySQL 엔진 아키텍처

---

<br/>
<br/>

# 1.1 MySQL의 전체 구조

---

<br/>

![사진](https://user-images.githubusercontent.com/109974940/225888946-5e05cdb4-1b7c-42b4-ab26-6ca0f8c37478.png)

- [출처](https://rrhh234cm.tistory.com/200)

<br/>
<br/>

## 1.1.1 MySQL 엔진

---

<br/>

- MySQL 엔진
  - 요청된 SQL 문장을 분석하거나 최적화하는 등 DBMS의 두뇌에 해당하는 처리를 수행

<br/>
<br/>

## 1.1.2 스토리지 엔진

---

<br/>

- 스토리지 엔진
  - 실제 데이터를 디스크 스토리지에 저장하거나 디스크 스토리지로부터 데이터를 읽어오는 부분은
    이 전담

<br/>

{: .prompt-info }
> MySQL 서버에서   
> MySQL 엔진은 하나지만   
> 스토리지 엔진은 여러 개를 동시에 사용할 수 있다.

<br/>

테이블이 사용할 스토리지 엔진을 지정하면 이후  
해당 테이블 의 모든 읽기 작업이나 변경 작업은 정의된 스토리지 엔진이 처리

````sql
CREATE TABLE test_table (fd1 INT, fd2 INT) ENGINE=INNODB;
````

<br/>

각 스토리지 엔진은 성능 향상을 위해   
키 캐시(MyISAM 스토리지 엔진)나   
InnoDB 버퍼 풀(InnoDB 스토리지 엔진)과 같은 기능을 내장하고 있다.  

<br/>
<br/>

## 1.1.3 핸들러 API

---

<br/>

- 핸들러 API
  - 핸들러 요청에서 사용되는 API   
  - InnoDB 스토리지 엔진 또한 이 핸들러 API를 이용해 MySQL 엔진과 데이터를 주고받음

<br/>

{: .prompt-info }
> 핸들러 요청  
> 　 : MySQL 엔진의 쿼리 실행기에서     
> 　　 데이터를 쓰거나 읽어야 할 때는 각 스토리지 엔진에 쓰기 또는 읽기를 요청  

<br/>

핸들러 API를 통해 얼마나 많은 데이터(레코드) 작업이 있었는지는 확인

```sql
SHOW GLOBAL STATUS LIKE 'Handler%';
```
``` 
+----------------------------+-------+
| Variable_name | Value |
+----------------------------+-------+
| Handler_commit | 2696 |
| Handler_delete | 184 |
| Handler_discover | 0 |
| Handler_external_lock | 15589 |
| Handler_mrr_init | 0 |
| Handler_prepare | 326 |
| Handler_read_first | 67 |
| Handler_read_key | 7731 |
| Handler_read_last | 10 |
| Handler_read_next | 8394 |
| Handler_read_prev | 0 |
| Handler_read_rnd | 0 |
| Handler_read_rnd_next | 13676 |
| Handler_rollback | 1 |
| Handler_savepoint | 0 |
| Handler_savepoint_rollback | 0 |
| Handler_update | 352 |
| Handler_write | 840 |
+----------------------------+-------+
18 rows in set (0.02 sec)
```

<br/>
<br/>

# 1.2 MySQL 스레딩 구조

---

<br/>

MySQL 서버는 프로세스 기반이 아니라 스레드 기반으로 작동 
- 포그라운드(Foreground) 스레드
- 백그라운드(Background) 스레드



<br/>


## 1.2.1 포그라운드 스레드(클라이언트 스레드)

<br/>
<br/>


## 1.2.2 백그라운드 스레드

<br/>
<br/>


# 1.3 메모리 할당 및 사용 구조

<br/>
<br/>


## 1.3.1 글로벌 메모리 영역

<br/>
<br/>


## 1.3.2 로컬 메모리 영역

<br/>
<br/>


# 1.4 플러그인 스토리지 엔진 모델

<br/>
<br/>


# 1.5 컴포넌트

<br/>
<br/>


# 1.6 쿼리 실행 구조

<br/>
<br/>


## 1.6.1 쿼리 파서

<br/>
<br/>


## 1.6.2 전처리기

<br/>
<br/>


## 1.6.3 옵티마이저

<br/>
<br/>


## 1.6.4 실행 엔진

<br/>
<br/>


## 1.6.5 핸들러(스토리지 엔진)

<br/>
<br/>


# 1.7 복제

<br/>
<br/>


# 1.8 쿼리 캐시

<br/>
<br/>


# 1.9 스레드 풀

<br/>
<br/>


# 1.10 트랜잭션 지원 메타데이터

<br/>
<br/>


---

(참고)

- Real MySQL 8.0: 개발자와 DBA를 위한 MySQL 실전 가이드

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>

<!--

❤️면접예상질문 ❤️

-->

