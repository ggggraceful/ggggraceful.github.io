---
title: /Database/ 정규화
author: ggggraceful
date: 2023-01-14
categories: [03.STUDY, Database]
tags: [STUDY]
---

<br/>
<br/>

## 정규화

---

Normalization

<br/>

- ```관계형 데이터베이스```의 설계에서  
  중복을 최소화하기 위해 데이터를 구조화하는 프로세스를 정규화라고 합니다.

- 정규화의 기본 목표
  - 관련이 없는 함수 종속성은 별개의 릴레이션으로 표현하는 것
  - 테이블 간에 중복된 데이터를 허용하지 않는다는 것
  - 중복된 데이터를 허용하지 않음으로써  
    :무결성(Integrity)를 유지할 수 있으며, DB의 저장 용량 역시 줄일 수 있다.

<br/>

{: .prompt-info }
> ✔️ 비정규화   
> 복잡한 쿼리 속도를 높이고 성능을 향상시키기 위해 테이블에 중복 데이터를 추가하는 프로세스입니다.

<br/>

{: .prompt-info}

>✔️ 관계형 데이터베이스(RDB)  
>  테이블, 행, 열의 정보를 구조화하는 방식입니다. RDB에는 테이블을 조인하여 정보 간 관계 또는 링크를 설정할 수 있는 기능이 있어, 여러 데이터 포인트 간의 관계를 쉽게 이해하고 정보를 얻을 수 있습니다.

<br/>
<br/>

## 정규화 장점

---

- 데이터베이스 변경 시 이상 현상(Anomaly)을 제거할 수 있다.
- 정규화된 데이터베이스 구조에서는 새로운 데이터 형의 추가로 인한 확장 시,  
  그 구조를 변경하지 않아도 되거나 일부만 변경해도 된다.
- 데이터베이스와 연동된 응용 프로그램에 최소한의 영향만을 미치게 되어 응용프로그램의 생명을 연장시킨다.
- 이상 현상의 발생 가능성을 줄일 수 있다.

<br/>
<br/>

## 정규화 단점

---

- 릴레이션의 분해로 인해 릴레이션 간의 JOIN연산이 많아진다.
- 질의에 대한 응답 시간이 느려질 수도 있다. 
- 데이터의 중복 속성을 제거하고 결정자에 의해 동일한 의미의 일반 속성이 하나의 테이블로 집약되므로 한  
  테이블의 데이터 용량이 최소화되는 효과가 있다.
- 따라서 데이터를 처리할 때 속도가 빨라질 수도 있고 느려질 수도 있다.
- 만약 조인이 많이 발생하여 성능 저하가 나타나면 반정규화(De-normalization)를 적용할 수도 있다.
- 연산 시간이 증가한다.


<br/>
<br/>

## 정규화 단계

---

이러한 테이블을 분해하는 정규화 단계는  
테이블을 어떻게 분해되는지에 따라 정규화 단계가 달라진다.

- 일반적으로 제1정규형부터 보이스/코드(BCNF) 정규형까지 단계별로 질행합니다.
- 정규화는 실제 데이터 값이 아닌 개념적 측면에서 수행되어야 합니다.
- 실제 정규화 과정은 정규형 순서와 다를 수 있습니다.  
  (상황에 따라 어떤 정규형은 건너 뛸 수도 있다.)

<br/>

![스크린샷 2023-01-15 오전 1 47 32](https://user-images.githubusercontent.com/109974940/212484489-2667a95c-2b48-460d-bcbd-180608a0f6dc.png)

<br/>

<details>
<summary> 제1 정규화 </summary>
<div markdown="1">

- 테이블의 컬럼이 원자값(Atomic Value, 하나의 값)을 갖도록 테이블을 분해하는 것 
  (각 컬럼이 하나의 속성만을 가져야 한다.)
- 하나의 컬럼은 같은 종류나 타입(type)의 값을 가져야 한다.
- 각 컬럼이 유일한(unique) 이름을 가져야 한다.
- 칼럼의 순서가 상관없어야 한다.

<br/>

정규화가 필요한 테이블

![1전](https://user-images.githubusercontent.com/109974940/212458791-cb950218-ff5d-46c7-bdce-70b3838498b8.png)

⬇️

정규화 이후 

![1후](https://user-images.githubusercontent.com/109974940/212458783-fb4f9c35-06c7-47f4-b3cd-6592fe40751b.png)

<span style="font-size: 12px; color: rebeccapurple">[(사진출처)](https://code-lab1.tistory.com/48)</span>

</div>
</details>

<br/>

<details>
<summary> 제2 정규화 </summary>
<div markdown="1">

- 제1 정규화를 진행한 테이블에 대해 완전 함수 종속을 만족하도록 테이블을 분해하는 것
- 모든 컬럼이 부분적 종속(Partial Dependency)이 없어야 한다.  
  == 모든 칼럼이 완전 함수 종속을 만족해야 한다.

<br/>

정규화가 필요한 테이블
![2전](https://user-images.githubusercontent.com/109974940/212458798-f5d8f466-7cbd-4cc1-8061-719460de79ab.png)

⬇️

정규화 후

![2후](https://user-images.githubusercontent.com/109974940/212458807-cd49caad-d0b7-42d3-ade1-18fe7428919a.png)

<span style="font-size: 12px; color: rebeccapurple">[(사진출처)](https://code-lab1.tistory.com/48)</span>

</div>
</details>

<br/>

<details>
<summary> 제3 정규화 </summary>
<div markdown="1">

- 제2 정규화를 진행한 테이블에 대해 이행적 종속을 없애도록 테이블을 분해하는 것
- 2 정규형을 만족해야 한다.
- 기본키를 제외한 속성들 간의 이행 종속성 (Transitive Dependency)이 없어야 한다.

<br/>

정규화가 필요한 테이블

![3전](https://user-images.githubusercontent.com/109974940/212458818-33164d75-5290-4a33-90a5-edf9888d06a7.png)

⬇️

정규화 후

![3후](https://user-images.githubusercontent.com/109974940/212458823-6cb6bf6d-2f73-4692-8d49-4ab849c69211.png)

<span style="font-size: 12px; color: rebeccapurple">[(사진출처)](https://code-lab1.tistory.com/48)</span>

</div>
</details>

<br/>

<details>
<summary> BCNF 정규화 </summary>
<div markdown="1">

- 제3 정규화를 진행한 테이블에 대해 모든 결정자가 후보키가 되도록 테이블을 분해하는 것
- 3정규형을 만족해야 한다. 
- 모든 결정자가 후보키 집합에 속해야 한다.

<br/>

정규화가 필요한 테이블

![-전](https://user-images.githubusercontent.com/109974940/212458829-61d96af8-7af4-47fb-90e3-17f57466fe0e.png)

⬇️

정규화 후

![-후](https://user-images.githubusercontent.com/109974940/212458834-9f15fafb-479b-4dbc-95ad-b8b338794d77.png)

<span style="font-size: 12px; color: rebeccapurple">[(사진출처)](https://code-lab1.tistory.com/48)</span>

</div>
</details>

<br/>

<details>
<summary> 제4 정규화 이상 </summary>
<div markdown="1">

![스크린샷 2023-01-14 오후 3 30 00](https://user-images.githubusercontent.com/109974940/212459208-345987f6-8ae5-4ef3-89d9-da9077c1f5eb.png)

<span style="font-size: 12px; color: rebeccapurple">[(사진출처)](https://code-lab1.tistory.com/48)</span>


보통 정규화는 BCNF 까지만 하는 경우가 많고,  
그 이상 정규화를 하면 정규화의 단점이 나타날 수도 있다.

</div>
</details>

<br/>
<br/>

## 역정규화

---

정규화를 거치면 릴레이션 간의 연산(JOIN 연산)이 많아지는데,  
이로인해 성능이 저하될 우려가 있습니다.

<br/>

- 역정규화를 하는 가장 큰 이유는  
  성능 문제가 있는(읽기작업이 많이 필요한) DB의 전반적인 성능을 향상시키기 위함입니다.
  
<br/>
<br/>

---

(참고)

- [데이터베이스 정규화(Normalization)란](https://hongcoding.tistory.com/147)
- [정규화](https://mangkyu.tistory.com/110)
- [[DB] 정규화(Normalization)란? 정규화 예시, 1NF, 2NF, 3NF, BCNF](https://code-lab1.tistory.com/48)

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>


<!--

❤️면접예상질문 ❤️

-->
