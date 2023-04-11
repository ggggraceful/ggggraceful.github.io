---
title: /Database/💬 MySQl/ 트랜잭션과 잠금
author: ggggraceful
date: 2023-03-30
categories: [03.STUDY, Database]
tags: [STUDY]
---

<br/>
<br/>

{: .prompt-tip }
> ✔️ 잠금(Lock)과 트랜잭션  
> - 잠금:  동시성을 제어하기 위한 기능  
> - 트랜잭션: 데이터의 정합성을 보장하기 위한 기능  

<br/>
<br/>

# 1 트랜잭션

---

<br/>

- 애플리케이션 개발에서 고민해야 할 문제를 줄여주는 아주 필수적인 DBMS의 기능  
- 작업의 완전성을 보장해 주는 것
- 논리적인 작업 셋을 모두 완벽하게 처리하거나, 처리하지 못할 경우  
  원상태로 복구해서 작업의 일부만 적용되는 현상(Partial update)이 발생하지 않게 만들어주는 기능

<br/>

- 트랜잭션을 지원하는 스토리지 엔진 : InnoDB
- 트랜잭션을 지원하지 않는 스토리지 엔진 : MyISAM, MEMORY 등

<br/>
<br/>

{: .prompt-info }
> ✔️ 트랜잭션 격리 수준 :  
> 하나의 트랜잭션 내에서 또는 여러 트랜잭션 간의 작업 내용을   
> 어떻게 공유하고 차단할 것인지를 결정하는 레벨을 의미한다.  

<br/>
<br/>

# 1.1 MySQL에서의 트랜잭션

---

<br/>

하나의 쿼리가 있든 두 개 이상의 쿼리가 있든 관계없이   
1. 논리적인 작업 set 자체가 100% 적용되거나(COMMIT을 실행했을 때)     
2. 아무것도 적용되지 않아야함(ROLLBACK 또는 트랜잭션을 ROLLBACK시키는 오류가 발생했을 때)   
을 보장해 주는 것

<br/>
<br/>

# 1.2 주의사항

---

<br/>

- 프로그램의 코드가 데이터베이스 커넥션을 가지고 있는 범위와   
  트랜잭션이 활성화 되어 있는 프로그램의 범위를 최소화하는 것이 좋음  
  (최소의 코드에만 적용하는 것이 좋음)

- 프로그램의 코드에서 라인 수는 한두 줄이라고 하더라도 네트워크 작업이 있는 경우에는   
  반드시 트랜잭션에서 배제해야 함

<br/>

➡️ 이러한 실수로 인해 DBMS 서버가 높은 부하 상태로 빠지거나   
   위험한 상태에 빠지는 경우가 발생할 수 있기 때문에 주의필요  

<br/>
<br/>

# 2 MySQL 엔진의 잠금

---

<br/>

MySQL에서 사용되는 잠금(거시적 분류)

1. MySQL 엔진 레벨
  -  MySQL 서버에서 스토리지 엔진을 제외한 나머지 부분

2. 스토리지 엔진 레벨
  - 모든 스토리지 엔진에 영향을 미치지만,  
    스토리지 엔진 레벨의 잠금은 스토리지 엔진 간 상호 영향을 미치지는 않음


<br/>
<br/>

MySQL 엔진 잠금
- 글로벌락
- 테이블락
- 네임드락
- 메타데이터락

<br/>
<br/>

# 2.1 글로벌 락(GLOBAL LOCK)

---

<br/>

```sql
FLUSH TABLES WITH READ LOCK
```

<br/>

InnoDB 스토리지 엔진은 트랜잭션을 지원하기 때문에   
일관된 데이터 상태를 위해 모든 데이터 변경 작업을 멈출 필요는 없다.  
MySQL 8.0부터는 InnoDB가 기본 스토리지 엔진으로 채택되면서 조금 더 가벼운 글로벌 락의 필요성이 생겼다.  

<br/>
<br/>

- 한 세션에서 글로벌 락을 획득하면   
  다른 세션에서 SELECT를 제외한 대부분의 DDL 문장이나 DML 문장을 실행하는 경우   
  글로벌 락이 해제될 때까지 해당 문장이 대기 상태로 남음

<br/>

- MySQL에서 제공하는 잠금 가운데 가장 범위가 큼
- 영향을 미치는 범위는 MySQL 서버 전체
- 작업 대상 테이블이나 데이터베이스가 다르더라도 동일하게 영향을 미침

<br/>

- 사용
  - 여러 데이터베이스에 존재하는 MyISAM이나 MEMORY 테이블에 대해  
    mysqldump로 일관된 백업을 받아야 할 때는 글로벌 락을 사용

<br/>
<br/>

{: .prompt-info }
> ✔️ 백업락  
> MySQL 8.0 버전부터는 Xtrabackup이나 Enterprise Backup과 같은   
> 백업 툴들의 안정적인 실행을 위해 백업 락이 도입
> - 특정 세션에서 백업 락을 획득하면   
>   모든 세션에서 다음과 같이 테이블의 스키마나 사용자의 인증 관련 정보를 변경할 수 없게 됨  
> - 일반적인 테이블의 데이터 변경은 허용  

<br/>
<br/>

# 2.2 테이블 락(Table Lock)

---

<br/>

- 개별 테이블 단위로 설정되는 잠금
- 테이블 데이터 동기화를 위한 잠금
- MyISAM뿐 아니라 InnoDB 스토리지 엔진을 사용하는 테이블도 동일하게 설정 가능

<br/>

- 명시적 또는 묵시적으로 특정 테이블의 락을 획득할 수 있음

<br/>
<br/>

## 명시적 테이블락 

---

<br/>

테이블락 명시적 명령어
```sql
LOCK TABLES table_name [ READ | WRITE ]
```

<br/>

- UNLOCK TABLES 명령으로 잠금을 반납(해제)
- 특별한 상황이 아니면 애플리케이션에서 사용할 필요가 거의 없음

<br/>
<br/>

## 묵시적 테이블락

---

<br/>

- MyISAM이나 MEMORY 테이블에 데이터를 변경하는 쿼리를 실행하면 발생
- MySQL 서버가 데이터가 변경되는 테이블에 잠금을 설정하고 데이터를 변경한 후,   
  즉시 잠금을 해제하는 형태로 사용됨  
- 쿼리가 실행되는 동안 자동으로 획득됐다가 쿼리가 완료 후 자동 해제
- InnoDB 테이블의 경우 스토리지 엔진 차원에서 레코드 기반의 잠금을 제공하기 때문에  
   단순 데이터 변경 쿼리로 인해 묵시적인 테이블 락이 설정되지 않음  
  (InnoDB 테이블에도 테이블 락이 설정되지만  
   대부분의 데이터 변경(DML) 쿼리에서는 무시되고 스키마를 변견하는 쿼리(DDL)의 경우에만 영향을 미침)

<br/>
<br/>

# 2.3 네임드 락(Named Lock)

---

<br/>

네임드락 함수
```sql
GET_LOCK() 
```

<br/>

- 사용자의 필요에 맞게 사용할 수 있는 락
- 임의의 문자열에 대해 잠금을 설정할 수 있음
- 단순히 사용자가 지정한 문자열(String)에 대해 획득하고 반납(해제)하는 잠금
- 네임드 락은 자주 사용되지는 않음

<br/>

- 사용
  - 레코드에 대해서 복잡한 요건으로 레코드를 변경하는 트랜잭션에 유용하게 사용
  - 여러 클라이언트가 상호 동기화를 처리해야 할 때  
    (데이터베이스 서버 1대에 5대의 웹 서버가 접속해서 서비스하는 상황에서   
     5대의 웹 서버가 어떤 정보를 동기화해야 하는 요건)

<br/>
<br/>

{: .prompt-info }
> ✔️ MySQL 8.0 버전  
> - 네임드 락을 중첩해서 사용 가능   
> - 세션에서 획득한 네임드 락을 한 번에 모두 해제하는 기능도 추가  

<br/>

# 2.4 메타데이터 락(Metadata Lock)은

---

<br/>

- 테이블의 구조를 잠그는 락
- 데이터베이스 객체(대표적으로 테이블이나 뷰 등)의 이름이나 구조를 변경하는 경우에 획득하는 잠금
- 명시적으로 획득하거나 해제할 수 있는 것이 아니고 테이블의 이름을 변경하는 경우 자동으로 획득하는 잠금
- RENAME TABLE 명령의 경우 원본 이름과 변경될 이름 두 개 모두 한꺼번에 잠금을 설정

<br/>
<br/>

# 3 InnoDB 스토리지 엔진 잠금

---

<br/>

- MySQL에서 제공하는 잠금과는 별개로 스토리지 엔진 내부에서 레코드 기반의 잠금 방식을 탑재
- 레코드 기반의 잠금 방식을 사용하기 때문에 MyISAM보다는 훨씬 뛰어난 동시성 처리를 제공
- 하지만 이원화된 잠금 처리 탓에   
  InnoDB 스토리지 엔진에서 사용되는 잠금에 대한 정보는   
  MySQL 명령을 이용해 접근하기가 상당히 까다로움

<br/>
<br/>

# 3.1 InnoDB 스토리지 엔진의 잠금

---

<br/>

- 레코드 기반의 잠금 기능을 제공
- 일반 상용 DBMS와는 조금 다르게 InnoDB 스토리지 엔진에서는   
  레코드와 레코드 사이의 간격을 잠그는 갭(GAP) 락이라는 것이 존재  

<br/>
<br/>

# 3.1.1 레코드 락(Record lock, Record only lock)

---

<br/>

- 레코드 자체만을 잠그는 것
- 다른 상용 DBMS의 레코드 락과 동일한 역할을 하지만  
  InnoDB 스토리지 엔진은 레코드 자체가 아니라 인덱스의 레코드를 잠근다는 차이를 가짐

<br/>
<br/>

# 3.1.2 갭 락

---

<br/>

- 코드 자체가 아니라 레코드와 바로 인접한 레코드 사이의 간격만을 잠그는 것
- 코드와 레코드 사이의 간격에 새로운 레코드가 생성(INSERT)되는 것을 제어

<br/>
<br/>

# 3.1.3 넥스트 키 락

---

<br/>

- 레코드 락과 갭 락을 합쳐 놓은 형태
- InnoDB의 갭 락이나 넥스트 키 락은   
  바이너리 로그에 기록되는 쿼리가 레플리카 서버에서 실행될 때   
  소스 서버에서 만들어 낸 결과와 동일한 결과를 만들어내도록 보장하는 것이 주 목적
- But 의외로 넥스트 키 락과 갭 락으로 인해 데드락이 발생하거나   
  다른 트랜잭션을 기다리게 만드는 일이 자주 발생  
  (가능하다면 바이너리 로그 포맷을 ROW 형태로 바꿔서 넥스트 키 락이나 갭 락을 줄이는 것이 좋음)

<br/>
<br/>

# 3.1.4 자동 증가 락

---

<br/>

MySQL에서는 자동 증가하는 숫자 값을 추출(채번)하기 위해   
AUTO_INCREMENT라는 칼럼 속성을 제공한다.  

<br/>

AUTO_INCREMENT 칼럼이 사용된 테이블에 동시에 여러 레코드가 INSERT되는 경우,   
저장되는 각 레코드는 중복되지 않고 저장된 순서대로 증가하는 일련번호 값을 가져야 한다.  

<br/>

InnoDB 스토리지 엔진에 서는 이를 위해 
내부적으로 AUTO_INCREMENT 락(Auto increment lock)이라고 하는 테이블 수준의 잠금을 사용한다.

<br/>
<br/>

- INSERT와 REPLACE 쿼리 문장과 같이 새로운 레코드를 저장하는 쿼리에서만 필요
- UPDATE나 DELETE 등의 쿼리에서는 걸리지 않음
- 다름 잠금들과 다르게 트랜잭션과 관계없이   
  INSERT나 REPLACE 문장에서 AUTO_INCREMENT 값을 가져오는 순간만 락이 걸렸다가 즉시 해제

<br/>
<br/>

# 3.2 인덱스와 잠금

---

<br/>

- InnoDB의 잠금은   
  `레코드를 잠그는 것이 아니라`    
  `인덱스를 잠그는 방식으로 처리`  
  (변경해야 할 레코드를 찾기 위해 검색한 인덱스의 레코드를 모두 락을 걸어야 함)  

<br/>
<br/>

## 예시

```sql
mysql> 
 UPDATE employees SET hire_date=NOW() 
                  WHERE first_name='Georgi' 
                        AND last_name='Klassen';
```

<br/>

employees 테이블에서   
first_name='Georgi'이고   
last_name='Klassen'인 사원의  
입사 일자를 오늘로 변경하는 쿼리를 실행했을 경우

<br/>

➡️ first_name인 employee가 200명이 경우  
'first_name='Georgi'인 200건의 레코드가 모두 잠기게 된다.  

<br/>

만약 조직의 규모가 커서 'first_name='Georgi'인 employee가 너무 많다면  
각 클라이언트 간의 동시성이 상당히 떨어져서  
한 세션에서 UPDATE 작업을 하는 중에는   
다른 클라이언트는 그 테이블을 업데이트하지 못하고 기다려야 하는 상황이 발생할 수 있다.  

<br/>
<br/>

![스크린샷 2023-04-07 오후 8 57 42](https://user-images.githubusercontent.com/109974940/230604958-c522c723-6a89-4557-b4f7-069317773bfa.png)

<br/>

만약 이 `테이블에 인덱스가 하나도 없다면`  
`테이블을 풀 스캔하면서 UPDATE 작업을 하게된다.`   
`이 과정에서 테이블에 있는 모든 레코드를 잠그게 된다.`  
이것이 MySQL의 방식이며, MySQL의 InnoDB에서 인덱스 설계가 중요한 이유 또한 이 때문이다.

<br/>

{: .prompt-tip }
> 인덱스가 있기 때문에 풀스캔하지 않고 UPDATE 할 수 있음

<br/>
<br/>


# 3.3 레코드 수준의 잠금 확인 및 해제

---

<br/>

테이블 잠금에서는 잠금의 대상이 테이블 자체이므로 쉽게 문제의 원인이 발견되고 해결될 수 있다.  

하지만 InnoDB 스토리지 엔진을 사용하는 테이블의 레코드 수준 잠금은  
테이블의 레코드 각각에 잠금이 걸리므로 그 레코드가 자주 사용되지 않는다면  
오랜 시간 동안 잠겨진 상태로 남아 있어도 잘 발견되지 않는다. 

MySQL 5.1부터는 레코드 잠금과 잠금 대기에 대한 조회가 가능해져    
쿼리 하나만 실행해 보면 잠금과 잠금 대기를 바로 확인 가능하다.

<br/>

> 1. 기존의 mysql
> : 각 트랜잭션이 어떤 잠금을 기다리고 있는지,   
>   기다리고 있는 잠금을 어떤 트랜잭션이 가지고 있는지를  
>   쉽게 메타 정보를 통해 조회 가능
> 
> 2. MySQL 5.1부터
> : information_schema라는 DB에  
>   INNODB_TRX라는 테이블과 INNODB_LOCKS, INNODB_LOCK_WAITS라는 테이블을 통해 
>   확인이 가능
> 
> 3. MySQL 8.0 버전부터
> : information_schema의 정보들은 조금씩 제거(Deprecated)되고 있으며, 
>   그 대신 performance_schema의 data_locks와 data_lock_waits 테이블로 대체

<br/>

##  performance_schema의 테이블을 이용해 잠금과 잠금 대기 순서를 확인하는 방법

---

<br/>

(예시)

```sql
mysql> SHOW PROCESSLIST;
+----+--------+----------+-----------------------------------------------------------+
| Id | Time | State | Info |
+----+--------+----------+-----------------------------------------------------------+
| 17 | 607 | | NULL |
| 18 | 22 | updating | UPDATE employees SET birth_date=NOW() WHERE emp_no=100001 |
| 19 | 21 | updating | UPDATE employees SET birth_date=NOW() WHERE emp_no=100001 |
+----+--------+----------+-----------------------------------------------------------+
```

<br/>

- 17번 스레드
  - 지금 아무것도 하지 않고 있음
  - 트랜잭션을 시작하고 UPDATE 명령이 실행 완료된 상태
  - But 아직 17번 스레드는 COMMIT을 실행하지는 않은 상태로
    업데이트한 레코드의 잠금을 그대로 가지고 있는 상태
  
- 18번 스레드가 그다음으로 UPDATE 명령을 실행
  - 잠금 대기로 인해 아직 UPDATE 명령을 실행 중인 것으로 표시

- 19번 스레드가 그다음으로 UPDATE 명령을 실행
  - 잠금 대기로 인해 아직 UPDATE 명령을 실행 중인 것으로 표시

<br/>
<br/>

(예시)

```sql
mysql> SELECT
 r.trx_id waiting_trx_id,
 r.trx_mysql_thread_id waiting_thread,
 r.trx_query waiting_query,
 b.trx_id blocking_trx_id,
 b.trx_mysql_thread_id blocking_thread,
 b.trx_query blocking_query
 FROM performance_schema.data_lock_waits w
 INNER JOIN information_schema.innodb_trx b
 ON b.trx_id = w.blocking_engine_transaction_id
 INNER JOIN information_schema.innodb_trx r
 ON r.trx_id = w.requesting_engine_transaction_id;
+---------+---------+-------------------+----------+----------+-------------------+
| waiting | waiting | waiting_query | blocking | blocking | blocking_query |
| _trx_id | _thread | | _trx_id | _thread | |
+---------+---------+-------------------+----------+----------+-------------------+
| 11990 | 19 | UPDATE employees..| 11989 | 18 | UPDATE employees..|
| 11990 | 19 | UPDATE employees..| 11984 | 17 | NULL |
| 11989 | 18 | UPDATE employees..| 11984 | 17 | NULL |
+---------+---------+-------------------+----------+----------+-------------------+
```
<br/>

17번 스레드가  
  가지고 있는 잠금을 해제하고,   
18번 스레드가  
  그 잠금을 획득하고,  
  UPDATE를 완료한 후,  
  잠금을 풀어야  
19번 스레드가  
  UPDATE를 실행할 수 있음을 의미  

<br/>

{: .prompt-info }
> - waiting _thread  
>  :현재 어떤 스레드를 기다리고 있는지 알려줌  
  
<br/>
<br/>

17번 스레드가 어떤 잠금을 가지고 있는지 더 상세히 확인하고 싶다면   
다음과 같이 performance_schema의   
data_locks 테이블이 가진 칼럼을 모두 살펴보면 된다.  

<br/>

```sql
 LOCK_TYPE: TABLE
 LOCK_MODE: IX
```

해당 테이블에 대해 IX 잠금(Intentional Exclusive)을 가지고 있음

<br/>

```sql
 LOCK_TYPE: RECORD
 LOCK_MODE: X,REC_NOT_GAP
```

- 해당 테이블의 특정 레코드에 대해서 쓰기 잠금을 가지고 있음  
- REC_NOT_GAP 표시가 있으므로   
  레코드 잠금은 갭이 포함되지 않은 순수 레코드에 대해서만 잠금을 가지고 있음

<br/>

강제종료 명령어

```sql
mysql> 
KILL <스레드 번호>;
```
<br/>
<br/>

# 4 MySQL의 격리 수준

---

<br/>

- 트랜잭션의 격리 수준(isolation level)
: 여러 트랜잭션이 동시에 처리될 때  
  특정 트랜잭션이 다른 트랜잭션에서 변경하거나 조회하는 데이터를 볼 수 있게  
  허용할지 말지를 결정하는 것

<br/>

|                  | DIRTY READ | NON-REPEATABLE | PHANTOM READ          |
|------------------|----|-------|-----------------------|
| READ UNCOMMITTED | 발생 | 발생  | 발생                    |
| READ COMMITTED   | 없음 | 발생  | 발생                    |
| REPEATABLE READ  | 없음 | 없음  | 발생 <br/> (InnoDB는 없음) |
| SERIALIZABLE     | 없음 | 없음  | 없음                    |

<br/>

{: .prompt-info }
> SQL-92 또는 SQL-99 표준에 따르면  
> REPEATABLE READ 격리 수준에서는  
> PHANTOM READ가 발생할 수 있지만,  
> InnoDB에서는 독특한 특성 때문에  
> REPEATABLE READ 격리 수준에서도  
> PHANTOM READ가 발생하지 않는다.

<br/>

## 사용

<br/>

- 일반적인 온라인 서비스 용도의 데이터베이스
: 주로 READ COMMITTED와 REPEATABLE READ 중 하나를 사용 

- 오라클 같은 DBMS
: 주로 READ COMMITTED 수준을 사용

- MySQL
: 주로 REPEATABLE READ 수준을 사용

<br/>
<br/>

# 4.1 READ UNCOMMITTED(DIRTY READ)

---

<br/>

- 일반적인 데이터베이스에서는 거의 사용하지 않음

<br/>

트랜잭션에서의 변경 내용이  
COMMIT이나 ROLLBACK 여부에 상관없이 다른 트랜잭션에서 보임.  

<br/>

- RDBMS 표준에서는  
  트랜잭션의 격리 수준으로 인정하지 않을 정도로 정합성에 문제가 많은 격리 수준  
  (MySQL을 사용한다면 최소한 READ COMMITTED 이상의 격리 수준을 사용할 것을 권장)

<br/>

- 더티 리드(Dirty read)
  - 어떤 트랜잭션에서 처리한 작업이 완료되지 않았는데도 다른 트랜잭션에서 볼 수 있는 현상
  - 데이터가 나타났다가 사라졌다 하는 현상을 초래하므로  
    애플리케이션 개발자와 사용자를 상당히 혼란스럽게 만듦  

<br/>

{: .prompt-info }
> 데이터 정합성  
> - 데이터가 서로 모순 없이 일관되게 일치해야 함
> - 중복 데이터를 많이 사용하면 데이터끼리 정합성을 맞추기 어려움
> - 비정규형을 사용해 아노말리 (anomaly : 이상현상)가 발생하면 정합성이 깨짐
> (정합성 훼손의 예시) "술은 마셨지만, 음주운전은 하지 않았다."


<br/>
<br/>

# 4.2 READ COMMITTED

---

<br/>

어떤 트랜잭션에서 데이터를 변경했더라도   
COMMIT이 완료된 데이터만 다른 트랜잭션에서 조회할 수 있음.  

<br/>

- 오라클 DBMS에서 기본으로 사용되는 격리 수준
- 온라인 서비스에서 가장 많이 선택되는 격리 수준
- 더티 리드(Dirty read) 같은 현상은 발생하지 않음

<br/>

- 어떤 트랜잭션에서 변경한 내용이 커밋되지 전까지는  
  다른 트랜잭션에서 그러한 변경 내역을 조회할 수 없기 때문에   
  언두 영역에 백업된 레코드를 가져와 보여줌  
  (커밋하면 그때부터는 다른 트랜잭션에서도 새로 변경된 값을 참고할 수 있게 됨)

<br/>

- NON-REPEATABLE READ (부정합의 문제)
  - REPEATABLE READ가 보장되지 않기 때문에  
    SELECT 쿼리가 실행될 때마다 다른 결과를 가져오는 문제 발생

<br/>
<br/>

## 트랜잭션 내에서 실행되는 SELECT문 / 트랜잭션 없이 실행되는 SELECT문

<br/>

READ COMMITTED 격리 수준 
 - 트랜잭션 내에서 실행되는 SELECT 문장과  
   트랜잭션 외부에서 실행되는 SELECT 문장의   
   차이가 별로 없다.

<br/>

REPEATABLE READ 격리 수준
- 기본적으로 SELECT 쿼리 문장도 트랜잭션 범위 내에서만 작동  
  (START TRANSACTION(또는 BEGIN) 명령으로   
  트랜잭션을 시작한 상태에서 온종일 동일한 쿼리를 반복해서 실행해도 동일한 결과가 나타남  
   (다른 트랜잭션에서 그 데이터를 변경하고 COMMIT을 실행했을 때도 동일))

<br/>
<br/>

# 4.3 REPEATABLE READ

---

<br/>

- MySQL의 InnoDB 스토리지 엔진에서 기본으로 사용되는 격리 수준
- 바이너리 로그를 가진 MySQL 서버에서는   
  최소 REPEATABLE READ 격리 수준 이상을 사용해야 함
- “NON-REPEATABLE READ” 부정합이 발생하지 않음

<br/>

- MVCC를 위해  
  언두 영역에 백업된 이전 데이터를 이용해  
  동일 트랜잭션 내에서는 동일한 결과를 보여줄 수 있게 보장
- REPEATABLE READ와 READ COMMITTED 모두  
  MVCC를 이용해 COMMIT되기 전의 데이터를 보여주고,  
  언두 영역에 백업된 레코드의 버전 차이가 있다.

<br/>

{: .prompt-info }
> MVCC(Multi Version Concurrency Control) 변경방식 :  
> InnoDB 스토리지 엔진은 트랜잭션이 ROLLBACK될 가능성에 대비해 변경되기  
> 전 레코드를 언두(Undo) 공간에 백업해두고 실제 레코드 값을 변경  

<br/>

InnoDB의 트랜잭션
- 고유한 트랜잭션 번호(순차적으로 증가하는 값)를 가짐  
- 언두 영역에 백업된 모든 레코드에는 변경을 발생시킨 트랜잭션의 번호 포함  
- 언두 영역의 백업된 데이터는  
  InnoDB 스토리지 엔진이 불필요하다고 판단하는 시점에 주기적으로 삭제

<br/>

하나의 레코드에
대해 백업이 하나 이상 얼마든지 존재할 수 있다. 한 사용자가 BEGIN으로 트랜잭션을 시작하고 장시간
트랜잭션을 종료하지 않으면 언두 영역이 백업된 데이터로 무한정 커질 수도 있다. 이렇게 언두에 백업
된 레코드가 많아지면 MySQL 서버의 처리 성능이 떨어질 수 있

<br/>

{: .prompt-info }
> 바이너리 로그    
> - MySQL 서버 인스턴스의 데이터 변경사항들에 대한 정보를 포함하는 로그 파일의 세트  
> - 에러코드, 바이너리 로그 자체에 대한 메타데이터 등 다양한 데이터가 같이 포함
> - 기본적으로 Transaction Commit 시에 기록되어지며, 데이터 변경 순서를 보장

<br/>
<br/>

# 4.4 SERIALIZABLE

---

<br/>

- 동시성이 중요한 데이터베이스에서는 거의 사용되지 않음
- 가장 단순한 격리 수준이면서 동시에 가장 엄격한 격리 수준
- 동시 처리 성능도 다른 트랜잭션 격리 수준보다 떨어짐
- 읽기 작업도 공유 잠금(읽기 잠금)을 획득해야만 하며,  
  동시에 다른 트랜잭션은 그러한 레코드를 변경하지 못함  
  ( 한 트랜잭션에서 읽고 쓰는 레코드를 다른 트랜잭션에서는 절대 접근할 수 없음)
- 일반적인 DBMS에서 일어나는 “PHANTOM READ”문제 발생하지 않음

<br/>
<br/>
---

(참고)

- [2. 트랜잭션과 잠금](https://velog.io/@sixhustle/mysql-transaction-isolation)

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>

<!--

❤️면접예상질문 ❤️

-->

