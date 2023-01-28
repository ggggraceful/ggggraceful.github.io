---
title: /Data structure/ Array, LinkedList
author: ggggraceful
date: 2023-01-12
categories: [03.STUDY, Data structure]
tags: [STUDY]
---

<br/>
<br/>

## 📌 Array(배열)

---

- 배열은 특정 크기만큼 연속된 메모리 공간에 데이터를 저장하는 자료구조  
- 메모리 공간에 필요한 크기의 메모리 영역을 미리 잡아놓고 사용하는 자료구조이기 때문에 
  선언 시 그 크기를 반드시 지정해야 한다.
- 배열도 객체이다. 

<br/>
<br/>

### 1. 배열의 장점
---

- 구조가 간단하여 사용하기 쉽다.
- 데이터를 읽어오는 시간(접근시간, access time)이 가장 빠르다.
  - index를 통해서 데이터에 빠른 접근이 용이하다.
  - 메모리상에서 연속적으로 저장되어 있는 특징을 갖기 때문이다.

<br/>
<br/>

### 2. 배열의 단점
---

- 배열의 크기는 처음 생성할 때 정하며 이후에는 변경할 수 없다.
  - 크기를 변경할 수 없어서, 새로운 배열을 생성해서 데이터를 복사해야한다.
  - 실행속도를 향상시키기 위해서는 충분히 큰 크기의 배열을 생성해야하므로 메모리가 낭비된다.

<br/>

- 비순차적인 데이터의 추가/삭제에 시간이 많이 소요된다.
  - 배열에 비해서 리스트 중간에 데이터를 추가하고 삭제하는 과정은 비교적 간단하지만,
  - 데이터 연결을 재구성 해야 하는 추가적인 작업 역시 필요하다.  
    (배열의 중간에 데이터를 추가하려면, 빈자리를 만들기 위해 다른 데이터들을 복사해서 이동시켜야 함)

<br/>

- 배열 중간에 있는 데이터가 삭제되면 공간낭비가 발생된다.

<br/>
<br/>

### 3. 언제 배열을 사용하는가

---

- 빠른 접근이 요구될 때
- 데이터의 삽입과 삭제가 적을 때
- 정적인 크기의 데이터를 다룰 때에 적합  
  (데이터의 양이 계속해서 늘어난다거나 바뀌는 경우에는 부적합)
- 데이터의 크기가 작을 때
- 데이터의 빈공간을 채우는 방법이 필요할 때
- 간단하게 데이터를 쌓고 싶을 때

<br/>
<br/>

### 4. 배열의 시간 복잡도

---

- 탐색 : O(1) / 순차적으로 탐색시에는 O(n)  
  (단, 접근하고자 하는 인덱스를 알고있어야 한다.)

- 삽입 및 삭제
  - 배열의 처음 또는 중간에 삽입 및 삭제: O(n) (삽입 지점 이후의 데이터를 옮겨야 하기 때문)
  - 배열의 끝에 삽입 및 삭제: O(1)

<br/>

  ![배열의 시간복잡도](https://user-images.githubusercontent.com/109974940/212147430-8595ab99-9a7b-48e5-b4ba-ed94182a168c.png)

<br/>
<br/>

## 📌 ArraysList(배열리스트)

---

- 배열의 단점을 보완한 ArrayList는  
  크기를 정해주지 않아도 되는 가변적으로 크기가 변하는 선형 리스트이다.
- Object(객체) 배열을 이용해서 데이터를 순차적으로 저장

- 배열과는 다르게 메모리를 연속적으로 사용하지 않는다.
- 일반적인 배열과 동일하게  
  순차 리스트이고(메모리가 연속적으로 배치),
  index를 이용해 내부의 객체를 관리한다.

- 데이터가 추가되어 저장 용량을 초과하면 자동으로 부족한 만큼 용량을 늘린다.
- 요소를 추가하면 index 0 부터 차례대로 저장된다.

- 데이터의 저장순서가 유지되고, 중복을 허용한다.


<br/>

![사진](https://user-images.githubusercontent.com/109974940/212241638-c6c01d7a-d780-4eab-a56c-cef30c6266d2.png)

![사진](https://user-images.githubusercontent.com/109974940/212241678-b275fb66-07f5-4275-89f5-28232a7e7056.png)

<br/>

- 기존의 Vector을 개선한 것으로  
  Vector의 구현원리와 기능적인 측면이 동일하다고 볼 수 있다.  
  - Array 개선 -> Vector
  - Vector 개선 -> Array List

<br/>

{: .prompt-info }
✔️Vector(벡터)  
　  
Vector는 미리 크기를 정해 선언해야하는 Array를 더 효율적으로 활용할 수 있게한 동적 배열구조 클래스이다.  
　  
-벡터의 장점  
　-마지막 위치를 추가/삭제는 쉬움  
　-구현이 용이  
　-중복을 허용하고, 랜덤적으로 직접 접근 가능 (index 사용)  
　  
-벡터의 단점  
　-중간에 삽입/삭제가 많은 상황에선 비효율적(배열과 마찬가지)  
　-다량의 데이터에서 검색이 느림  
　  
--️언제 벡터를 사용하는가  
　-저장하려는 데이터의 개수가 가변적일 때  
　-컴파일 시점에 개수를 모를 때  
　-중간에 데이터를 삽입/삭제할 일이 없고,  
　　마지막에 추가/삭제 정도만 있을 때  
　-랜덤하게 데이터 접근을 허용하고 싶을 때  
　  
-벡터의 시간복잡도  
　-탐색 : O(1)  
　-삽입 및 삭제  
　　-탐색과 맨뒤의 요소 삽입 및 삭제: O(1)  
　　-맨 뒤나 맨 앞이 아닌 요소를 삭제하고 삽입: 0(n)  


<br/>
<br/>

### 1. 배열리스트의 장점

---

- 데이터의 참조가 쉽다.  
  (인덱스값을 기준으로 어디든 한번에 참조 가능)

<br/>
<br/>

### 2. 배열리스트의 단점

---

- 배열의 길이가 정해져 있어 변경이 불가능하다.
- 중간의 특정 index에 데이터를 추가하거나 삭제하면  
  index 이후에 위치한 데이터를 모두 한칸씩 앞뒤로 옮겨주어야해 비효율적이다.

<br/>
<br/>

### 3. 언제 배열리스트를 사용하는가

---

- 데이터의 크기가 가변적일 때
- 중간에 데이터를 삽입한다거나 삭제하는 경우가 거의 없을 때

<br/>
<br/>


### 💚 4. 배열리스트의 시간복잡도

---

<br/>
<br/>
<br/>

## 📌 LinkedList(연결리스트)

---

- 여러 개의 노드들이 순차적으로 연결된 형태를 갖는 자료구조
- 연속적인 메모리 위치에 저장되지 않는 선형 구조의 자료구조
- 연속된 메모리를 사용하지 않기 때문에 포인터를 사용해 메모리들을 연결한다. 
- 각 노드는 데이터와 다음 노드를 가리키는 포인터로 이루어져 있다.
- 배열의 단점을 극복하기 위해 만들졌다.
- 불열속적으로 존재하는 데이터를 서로 연결한 형태로 구성

#### 노드(Node)❓

{: .prompt-info }

노드(Node)  
<br/>
컴퓨터 과학에 쓰이는 기초적인 단위이다. 노드는 대형 네트워크에서는 장치나 데이터 지점(data point)을 의미한다. 개인용컴퓨터, 휴대전화, 프린터와 같은 정보처리 장치들이 노드이다.  
　- Node = Data + Pointer    
　- 첫번째 노드: 헤드(Head)   
　- 마지막 노드:  테일(Tail)  

<br/>
<br/>

### 1. 연결리스트의 장점
---

- 데이터의 크기가 유동적이다.
- 미리 메모리 영역 할당이 필요 없다.
- 노드가 연결된 구조이기 때문에 삽입과 삭제가 용이하다.
 :새로운 데이터를 추가할 때는  
  새로운 요소를 생성한 다음
  추가하고자하는 위치의 이전요소의 참조를 새로운 요소에 대한 참조로 변경해주고,
  새로운 요소가 그 다음 요소를 참조하도록 변경하기만 하면 되므로
  처리속도가 매우 빠르다
- 이동방향이 단방향이기 때문에 다음 요소에 대한 접근이 쉽다.


<br/>
<br/>

### 2. 연결리스트의 단점
---

- 특정 데이터를 찾기 위해서는 head 부터 순차적으로 데이터 접근 속도가 느리다.
  - 임의접근이 불가능하여 처음부터 탐색을 진행해야 함
  - 다음 요소에 대한 접근은 쉽지만, 이전요소에 대한 접근은 어려움
    (이점을 보완한 것으로 doubly linked list, doubly circular linked list가 있음)

{: .prompt-info }

✔️doubly linked list
<br/>
　-링크드리스트에 참조변수를 하나 더 추가하여 <br/>
　　다음 요소에 대한 참조뿐 아니라 <br/>
　　이전 요소에 대한 참조도 가능하게 한 것<br/>
　-이외에는 링크드 리스트와 같다. <br/>
✔️doubly circular linked list
<br/>
　-더블 링크드리스트의 접근성을 보다 향상 시킨 것  <br/>
　-단순히 더블 링크드 리스트의 첫번째 요소와 마지막 요소를 서로 연결시킨 


<br/>

- 배열에 비해서 리스트 중간에 데이터를 추가하고 삭제하는 과정은 비교적 간단하지만,
  데이터 연결을 재구성 해야 하는 추가적인 작업 역시 필요하다.  
- 메모리 할당/삭제 때문에 성능이 저하될 수 있다.
  
<br/>

- 다음 노드를 가리키는 포인터를 한번에 담을 추가 공간이 있어야 하기 때문에  
  공간 효율이 좋지 않다.
- 포인터 공간이 하나이상 추가되어서 메모리가 크다.

<br/>
<br/>

### 3. 언제 연결리스트를 사용하는가

---

<br/>

- 삽입과 삭제 연산이 잦을 때
- 검색 빈도가 적을 때

<br/>
<br/>

### 4. 연결리스트의 종류

---

1. 단순 연결 리스트

   ![스크린샷 2023-01-13 오후 2 24 46](https://user-images.githubusercontent.com/109974940/212243857-252c38b4-96db-4d3f-9ac3-50ad1c97a9c0.png)


2. 이중 연결 리스트:  
   데이터 앞뒤로 이동 및 탐색 가능

   ![스크린샷 2023-01-13 오후 2 25 03](https://user-images.githubusercontent.com/109974940/212243880-a4b01cc5-06c8-48ee-a91e-13f325bf1439.png)


3. 원형 연결 리스트:  
   마지막 노드의 포인터가 첫번째 노드를 가리킴

   ![스크린샷 2023-01-13 오후 2 25 13](https://user-images.githubusercontent.com/109974940/212243909-24b6282f-6074-4a46-9643-cd4d18d1128d.png)


<br/>
<br/>

### 5. 연결리스트의 시간 복잡도
---

- 탐색: O(n)
  
- 삽입 및 삭제: 삽입과 삭제 자체는 O(1) 이다.
  - 연결리스트의 처음에 삽입 및 삭제: O(1)
  - 연결리스트의 중간에 삽입 및 삭제: O(n) (탐색시간 소요)
  - 연결리스트의 끝에 삽입 및 삭제:
    - 끝을 가리키는 별도의 포인터를 갖는 경우: O(1)
    - 끝을 가리키는 별도의 포인터를 갖지 않는 경우: O(n) (탐색시간 소요)
    
  <br/>

  ![연결리스트의 시간 복잡도](https://user-images.githubusercontent.com/109974940/212240593-3e71c3b3-7fa4-48d1-8155-aa23754f383f.png)


<br/>
<br/>
<br/>


## 📎 Array / LinkedList 비교

---

|  |배열|연결리스트|
|--|---|-------|
|장점|인덱스를 통한 빠른 접근이 가능하다.|삽입과 삭제가 용이하다.|
|단점|- 삽입과 삭제가 오래 걸린다.<br/>- 배열 중간에 있는 데이터가 삭제되면,<br/> 　공간 낭비가 발생한다.|	임의 접근이 불가능하여, <br/>처음부터 탐색을 진행해야 한다.|
|용도|빠른 접근이 요구되고, <br/>데이터의 삽입과 삭제가 적을 때|삽입과 삭제 연산이 잦고,<br/> 검색 빈도가 적을 때|

<br/>
<br/>


## 📎 ArrayList / LinkedList 비교

---

|  |  ArrayList(배열리스트)  |  Linked List(연결리스트)  |
|--|----------------------|------------------------|
|특징|-메모리가 연속적으로 배치<br/>-순차적인 추가삭제는 더 빠름<br/>-비효율적인 메모리사용 |-배열의 단점을 극복하기 위해 만듬<br/>-데이터가 많을수록 접근성이 떨어짐|
|장점|1. 데이터의 참조가 쉽다. <br/> 　즉, 인덱스값을 기준으로 <br/>　어디든 한번에 참조 가능|1. 크기가 유동적이다<br/> 2. 메모리 중간에 삽입/삭제가<br/>　 자유롭다.|
|단점|1. 배열의 길이가 정해져있다.<br/>　(변경 불가) <br/> 2. 중간에 메모리의 삽입과 삭제가 <br/>　번거롭다.|1. 포인터 공간이 하나이상이 <br/>　추가되어서 메모리가 크다. <br/> 2. 메모리 할당/삭제때문에 성능 저하 |
|읽기<br/>(접근시간)|빠르다 |느리다|
|추가/삭제|느리다|빠르다|


<br/>
<br/>

### 💚 ArrayList / LinkedList 사용법(메소드 등)

---

<br/>
<br/>

### 💚 ArrayList / LinkedList  내부 구현 분석

---

<br/>
<br/>




## 📎 java.util.Arrays 패키지

---

- java.util.Arrays는  java.util 패키지에 포함되므로,  
  반드시 import 문으로 java.util 패키지를 불러오고 나서 사용해야 한다.
- Arrays 클래스는 정렬(sorting)이나 탐색(searching)과 같은 배열관리 메소드를 포함하고 있다. 
- Arrays 클래스의 메소드들은 특정 배열 참조값이 null값이면 nullPointerException이 적용된다. 
- 배열을 목록으로 볼 수 있도록 하는 static factory 또한 포함하고 있다.
- Arrays 클래스의 모든 메소드는 클래스 메소드(static method)이므로,  
  객체를 생성하지 않고도 바로 사용할 수  있다. 

```java
import java.util.Arrays;

public class ArraysEx {

  public static void main(String[] args) {

    // 배열 선언
    int[] array = { 1, 0, 4, 5, 7, 2, 8, 6, 9, 3 };

    // 배열을 출력할때 for문을 이용하지만 
        // Arrays.toString()을 이용하면 간단하게 출력이 가능하다.
        System.out.println("-----Arrays.toString()-----");
        System.out.println(array);
        System.out.println(Arrays.toString(array));
        System.out.println();
         
        // Arrays.sort()를 이용하면 오름차순 정렬이 되고 기존의 값을 변경 시킨다.
        System.out.println("-----Arrays.sort()-----");
        Arrays.sort(array);
        System.out.println(Arrays.toString(array));
        System.out.println();
         
        // Arrays.binarySearch()를 이용하면 해당 특정값을 찾아준다. 
        // 검색 결과가 없거나 오류시 음수값을 반환한다.
        // 검색하기 전에는 오름차순으로 정렬되어있어야한다. -> 안그럼 음수값을 반환
        System.out.println("-----Arrays.binarySearch()-----");
        System.out.println(Arrays.binarySearch(array, 6));
        System.out.println(Arrays.binarySearch(array, 10));
        System.out.println();
         
        // Arrays.equals()를 이용하면 두 배열을 비교할 수 있다. 같으면 true, 틀리면 false
        int[] a1 = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
        int[] a2 = { 0, 1, 1, 1, 1, 1 };
        System.out.println("-----Arrays.equals()-----");
        System.out.println(Arrays.equals(array, a1));
        System.out.println(Arrays.equals(array, a2));
        System.out.println();
         
        // Arrays.fill()를 이용하면 배열을 초기화할 수 있다.
        System.out.println("-----Arrays.fill()-----");
        Arrays.fill(array, 0);
        System.out.println(Arrays.toString(array));
        Arrays.fill(array, 1);
        System.out.println(Arrays.toString(array));
    }
}
```

```
-----Arrays.toString()-----
[I@14db9842]
[1, 5, 4, 7, 6, 2, 0, 9, 3, 8]

-----Arrays.sort()-----
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

-----Arrays.binarySearch()-----
6
-11

-----Arrays.equals()-----
true
false

-----Arrays.fill()-----
[0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
[1, 1, 1, 1, 1, 1, 1 ,1 ,1 ,1]

```
<span style="font-size: 12px; color: rebeccapurple"> [(출처) - [ Java ] 배열 다루기 ( Arrays Class )](https://codeman77.tistory.com/64) </span>

<br/>
<br/>


## 📎 new ArrayList()와 List.of()

---

```java
import java.util.ArrayList; // new ArrayList<>()
import java.util.Arrays; // Arrays.asList()
import java.util.List;	// List.of()
```
<br/>

|  |원소를 추가/삭제|set 사용 가능|null|
|new ArrayList<>()|가능|	가능|null을 가질 수 있음|
|Arrays.asList()|불가능|가능|null을 가질 수 있음|
|List.of()	|불가능|불가능|null을 가질 수 없음|

<br/>

- ArrayList<>()
  - List값을 하나만 넣으려면 List.of()를 감싸서 넣으면 된다.
  - new ArrayList<>()를 사용하여 컬렉션 생성 시, 새로운 주소값으로 할당하여 의도치 않는 변화를 막는다.

<br/>

- Arrays.asList()
  - 참조한 원본 배열의 값이 바뀌면 List의 값도 바뀌고, List의 값이 바뀌면 원본 배열의 값도 바뀐다.

<br/>

- List.of()
  - 참조한 원본 배열의 값이 바뀌어도 List의 값은 바뀌지 않는다.

<br/>
<br/>

- 사용  
  - 테스트 코드에서 배열의 size가 변하면 안 되거나 변할 필요가 없을 때 List.of()를 사용한다.  
  - 그런데 null값을 테스트 해야한다면 Arrays.asList()를 사용한다.  

<br/>
<br/>

## 📎 배열의 깊은 복사, 얕은 복사

---

- Java의 복사
  1. 얕은 복사(Shallow copy):  
     원본 배열이나 복사된 배열이 변경될 때 상대 배열의 값이 같이 변경된다.
  2. 깊은 복사(Deep copy):  
     원본 배열이나 복사된 배열이 변결될 때 서로간의 값은 바뀌지 않는다.

<br/>

- primitive type의 변수:  
  얕은 복사로도 문제 없이 진행된다.
- reference type(객체, 배열 등)의 변수:  
  깊은 복사를 사용해야지만 객체의 실제 데이터를 복사할 수 있다.

<br/>

#### 1. 얕은 복사(Shallow Copy)

```java
int[] a = {1, 2, 3, 4};
int[] b = a;
System.out.println(Arrays.toString(a)); // [1, 2, 3, 4]

System.out.println(Arrays.toString(b)); // [1, 2, 3, 4]


// 원본 배열 값 변경

a[1] = 10;
System.out.println(Arrays.toString(a)); // [1, 10, 3, 4]

System.out.println(Arrays.toString(b)); // [1, 10, 3, 4]


// 복사한 배열 값 변경

b[3] = 1111;
System.out.println(Arrays.toString(a)); // [1, 10, 3, 1111]

System.out.println(Arrays.toString(b)); // [1, 10, 3, 1111]
```

얕은 복사에서는 =연산자를 사용해 해당 변수에 담겨있는 값을 복사한다. 배열의 경우 해당 변수에 heap의 데이터를 가리키는 참조값이 저장되어있기 때문에 참조값이 복사되어 같은 원본 배열을 가리키게 되는 것이다.

<br/>
<br/>

#### 2. 깊은 복사(Deep Copy)

```java
int[] a = {1, 2, 3, 4};
int[] b = new int[a.length]; 
for (int i = 0; i < a.length; i++) {
    b[i] = a[i];
}
System.out.println(Arrays.toString(a)); // [1, 2, 3, 4]

System.out.println(Arrays.toString(b)); // [1, 2, 3, 4]


// 원본 배열 값 변경

a[1] = 10;
System.out.println(Arrays.toString(a)); // [1, 10, 3, 4]

System.out.println(Arrays.toString(b)); // [1, 2, 3, 4]


// 복사한 배열 값 변경

b[3] = 1111;
System.out.println(Arrays.toString(a)); // [1, 10, 3, 4]

System.out.println(Arrays.toString(b)); // [1, 2, 3, 1111]
```

이렇게 for문을 이용해 복사를 하는 방법도 있지만 java에서 지원하는 다양한 메소드(method)들을 활용하면 더 편하게 깊은 복사를 할 수 있다.

- [다양한 복사 메서드 참고링크](https://seoyoung2.github.io/java/2021/01/21/java-copy.html)



<br/>
<br/>


## 📎 Array / Array List / LinkedList 사용하면 좋을 데이터의 예시와 이유

---

✔️ 순차적으로 추가/삭제하는 경우: Array가 LinkedList보다 빠르다.  
✔️ 중간 데이터를 추가/삭제하는 경우: LinkedList가 ArrayList보다 빠르다.

<br/>
<br/>

---

( 참고링크 & 관련내용 )

- [배열과 연결리스트 (Array & LinkedList)](https://hongcoding.tistory.com/74)
- [[자료구조] 배열 Array, 배열 리스트 ArrayList, 연결 리스트 LinkedList](https://velog.io/@nnnyeong/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EB%B0%B0%EC%97%B4-Array-%EB%B0%B0%EC%97%B4-%EB%A6%AC%EC%8A%A4%ED%8A%B8-ArrayList-%EC%97%B0%EA%B2%B0-%EB%A6%AC%EC%8A%A4%ED%8A%B8-LinkedList)
- [노드](https://ko.wikipedia.org/wiki/%EB%85%B8%EB%93%9C_(%EC%BB%B4%ED%93%A8%ED%84%B0_%EA%B3%BC%ED%95%99))
- [배열리스트(Array List)와 연결리스트(Linked List)의 차이](https://bozeury.tistory.com/entry/%EB%B0%B0%EC%97%B4%EB%A6%AC%EC%8A%A4%ED%8A%B8Array-List%EC%99%80-%EC%97%B0%EA%B2%B0%EB%A6%AC%EC%8A%A4%ED%8A%B8Linked-List%EC%9D%98-%EC%B0%A8%EC%9D%B4)
- [다양한 복사 메서드](https://seoyoung2.github.io/java/2021/01/21/java-copy.html)
- [Arrays 클래스](http://www.tcpschool.com/java/java_api_arrays)
- [java.util.Arrays](https://docs.oracle.com/javase/7/docs/api/java/util/Arrays.html)
- [java.util.Arrays](http://www.incodom.kr/Java/java.util.Arrays)
- [[ Java ] 배열 다루기 ( Arrays Class )](https://codeman77.tistory.com/64)
- [배열(array), 행렬(matrix), 벡터(vector)에 대해 알아보자](https://velog.io/@mjk3136/%ED%96%89%EB%A0%AC-%EB%BF%8C%EC%85%94%EB%B2%84%EB%A6%AC%EA%B8%B0)
- [vector와 array의 차이](https://velog.io/@dik654/vector%EC%99%80-array%EC%9D%98-%EC%B0%A8%EC%9D%B4)
- [vector](https://bconfiden2.tistory.com/4)
- [C++에서의 자료구조 Array 대신 Vextor를 쓰는 이유](https://luv-n-interest.tistory.com/975)
- [자료구조STL vector 1탄](https://jhnyang.tistory.com/230)
- [자료구조: Linked List 대 ArrayList - 넥스트리소프트](https://www.nextree.co.kr/p6506/)

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>

<!--

❤️면접예상질문 ❤️

-->
