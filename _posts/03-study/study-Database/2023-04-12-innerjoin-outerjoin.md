---
title: /Database/ SQL join
author: ggggraceful
date: 2023-04-12
categories: [03.STUDY, Database]
tags: [study, database]
---

<br/>
<br/>

{: .prompt-tip }
> 중복이 없는 서로 다른 두 컬럼을 JOIN한다고 가정했을 때  
>   
> - inner join : 교집합  
> - outer join : 합집합  

<br/>
<br/>

- [sql join](https://user-images.githubusercontent.com/109974940/231751883-5bc1f827-ecc2-4191-8c53-b9d687f5eafd.png)

<br/>
<br/>

# 두 개의 테이블이 있다고 가정 

| A   | B   |
|-----|-----|
| 1   | 3   |
| 2   | 4   |
| 3   | 5   |
| 4   | 6   |

<br/>
<br/>

# Inner join

```sql
select * from a INNER JOIN b on a.a = b.b;
select a.*,b.*  from a,b where a.a = b.b;
```

| a   | b   |
|-----|- ----|
| 3   | 3   |
| 4   | 4   |

<br/>
<br/>

# Left outer join

```sql
select * from a LEFT OUTER JOIN b on a.a = b.b;
select a.*,b.*  from a,b where a.a = b.b(+);
```

| a   | b    |
|-----|------|
| 1   | null |
| 2   | null |
| 3   | 3    |
| 4   | 4    |

<br/>
<br/>

# Right outer join

```sql
select * from a RIGHT OUTER JOIN b on a.a = b.b;
select a.*,b.*  from a,b where a.a(+) = b.b;
```

| a    | b   |
|------|-----|
| 3    | 3   |
| 4    | 4   |
| null | 5   |
| null | 6   |

<br/>
<br/>

# Full outer join

```sql
select * from a FULL OUTER JOIN b on a.a = b.b;
```

| a    | b    |
|------|------|
| 1    | null |
| 2    | null |
| 3    | 3    |
| 4    | 4    |
| null | 6    |
| null | 5    |

<br/>
<br/>

---

(참고)

- [[SQL] INNER 조인과 OUTER조인이 무엇인가요?](https://stanleykou.tistory.com/entry/SQL-INNER-%EC%A1%B0%EC%9D%B8%EA%B3%BC-OUTER%EC%A1%B0%EC%9D%B8%EC%9D%B4-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80%EC%9A%94)

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>

