---
title: /Data structure/ 💚 HashSet, HashMap, TreeSet, TreeMap
author: ggggraceful
date: 2023-02-14
categories: [03.STUDY, Data structure]
tags: [STUDY]
---

<br/>
<br/>

# Set, Map / Hash, Tree

---

<br/>

|          | set | Map |
|----------|-----|-----|
| 자료형태     |  Value 만 존재   |  Key, Value 쌍으로 존재   |
| 중복여부     |  중복 불가  |  Key값 중복 불가   |
| contains |  contains(value)   |  containsKey(key)   |
| get      |  불가   | get(key)    |
      
<br/>    

- Set
  - contains 메소드로 값의 존재 여부만 확인할 수 있어 특정 요소를 get하려면 iterator를 통해 얻어야 함
- Map
  - key값을 통해 해당하는 value를 바로 얻을 수 있음

<br/>    
 
|  |  Hash   |  Tree   |
|--|-----|-----|
| 순서 |  순서 없음   | 정렬 순서 유지    |
| 시간 복잡도 | O(1)    | O(log n)    |
                                
<br/>    

- Hash와 Tree는 전혀 다른 내부 구조를 띄고 있기 때문에 시간 복잡도가 다르다.

- Hash : 순서를 유지하지 않는 대신 빠른 시간을 보장
- Tree : 트리 구조를 통해 순서를 유지하기 때문에 약간 시간이 느림

<br/>

{: .prompt-tip }
> HashSet :  속도가 빠르고, Value만 존재, 존재 여부만 판별 가능  
> HashMap : 속도가 빠르고, Key·Value 존재, get 가능  
> TreeSet : 정렬 순서 유지, Value만 존재, 존재 여부만 판별 가능  
> TreeMap : 정렬 순서 유지, Key·Value 존재, get 가능  

<br/>
<br/>

![스크린샷 2023-02-14 오후 1 55 32](https://user-images.githubusercontent.com/109974940/218642921-f3f8c43e-a3f4-4625-bc05-aad8aa2cd7bb.png)

<br/>
<br/>

# TreeSet, TreeMap

---

<br/>

컬렉션 프레임워크는 검색 기능을 강화시킨 TreeSet과 TreeMap을 제공하고 있다.  
TreeSet은 Set컬렉션이고, TreeMap은 Map컬렉션이다.  
이 컬렉션들은 이진 트리(binary tree)를 이용해서 계층적 구조(Tree 구조)를 가지면서 객체를 생성한다.  

<br/>

> ✔️ 이진 트리 구조  
> - 이진 트리(binary tree)는 여러 개의 노드(node)가 트리 형태로 연결된 구조로,  
>   루트 노트(root node)라고 불리는 하나의 노드에서부터 시작해서  
>   각 노드에 최대 2개의 노드를 연결할 수 있는 구조를 가지고 있다.  
> - 위아래로 연결된 두 노드를 부모-자식관계에 있다고 하며 
>   위의 노드를 부모 노드, 아래의 노드를 자식 노드라 한다.   
> - 하나의 부모 노드는 최대 2 개의 자식 노드와 연결될 수 있다.  
> - 이진 트리는 부모 노드의 값보다 작은 노드는 왼쪽에 위치시키고, 부모 노드의 값보다 큰 노드는 오른쪽에 위치시킨다.  
>   (숫자가 아닌 문자를 저장할 경우에는 문자의 유니코드 값으로 비교한다.)
> - Tree traversal(트리 순회)  
>   v: 노드 방문 ,L: 왼쪽 부분트리 운행, R: 오른쪽 부분트리 운행
>   - Pre-Order(전 순회) : vLR  
>   - In-Order(중 순회) : LvR  
>   - Post-Order(후 순회) LRv  

<br/>

- [이 블로그의 다른 글 - tree](https://ggggraceful.github.io/posts/tree/)

<br/>
<br/>

# TreeSet

---

<br/>

TreeSet은 이진 트리(binary tree)를 기반으로 한 Set 컬렉션이다.   
하나의 노드는 노드값인 value와 왼쪽과 오른쪽 자식 노드를 참조하기 위한 두 개의 변수로 구성된다.  
TreeSet에 객체를 저장하면 자동으로 정렬되는데   
부모값과 비교해서 낮은 것은 왼쪽 자식 노드에, 높은 것은 오른쪽 자식 노드에 저장된다.  

<br/>

```java
TreeSet<E> treeSet = new TreeSet<E>();
TreeSet<String> treeSet = new TreeSet<>();
```

<br/>
<br/>

## TreeSet이 가지고 있는 메소드

---

<br/>

|리턴 타입  | 	메소드    | 설명                                                        |
|---|---------|-----------------------------------------------------------|
| E | first() | 제일 낮은 객체를 리턴                                              |
| E | last()        | 	제일 높은 객체를 리턴                                             |
| E | lower(E e)        | 	주어진 객체보다 바로 아래 객체를 리턴                                    |
| E | higher(E e)       | 주어진 객체보다 바로 위 객체를 리턴                                      |
| E | floor(E e)        | 주어진 객체와 동등한 객체가 있으면 리턴, <br/>만약 없다면 주어진 객체의 바로 아래의 객체를 리턴 |
| E | ceiling(E e)       | 주어진 객체와 동등한 객체가 있으면 리턴, 만약 없다면 주어진 객체의 바로 위의 객체를 리턴                                                          |
| E | pollFirst()        | 	제일 낮은 객체를 꺼내오고 컬렉션에서 제거함                                                          |
| E | pollLast()	        |  제일 높은 객체를 꺼내오고 컬렉션에서 제거함                                                         |
                                                      |

<br/>
<br/>

## TreeSet이 가지고 있는 정렬 메소드

---

<br/>

|리턴 타입  | 	메소드    | 설명                                                        |
|---|---------|-----------------------------------------------------------|
| Iterator<E> |  descendingIterator()       |  내림차순으로 정렬된 Iterator를 리턴                                                         |
| NavigableSet<E> | descendingSet()        |  내림차순으로 정렬된 NavigableSet을 반환   |

<br/>

```java
NavigableSet<E> descendingSet = treeSet.descendingSet();
NavigableSet<E> ascendingSet = descendingSet.descendingSet(); // 두번 호출
```

<br/>
<br/>

# TreeSet이 가지고 있는 범위 검색과 관련된 메소드

---

<br/>

|리턴 타입  | 	메소드    | 설명                                                                                 |
|---|---------|------------------------------------------------------------------------------------|
|NavigableSet<E>|	headSet(E toElement, boolean inclusive)| 주어진 객체보다 낮은 객체들을 NavigableSet으로 리턴. <br/> 주어진 객체 포함 여부는 두번째 매개값에 따라 달라짐.           |
|NavigableSet<E>|tailSet(E fromElement, boolean inclusive)| 주어진 객체보다 높은 객체들을 NavigableSet으로 리턴.<br/>  주어진 객체 포함 여부는 두번째 매개값에 따라 달라진다.          |
|NavigableSet<E>|subSet<br/>(E fromElement, boolean fromInclusive,<br/> E toElement, boolean toInclusive)| 시작과 끝으로 주어진 객체 사이의 객체들을 NavigableSet으로 리턴. <br/> 시작과 끝 객체 포함여부는 두번째, 네 번째 매개값에 따라 달라진다. |

<br/>
<br/>

# TreeMap

---

<br/>

TreeMap도 TreeSet처럼 이진 트리를 기반으로 한 Map 컬렉션이다.  
TreeSet과의 차이점은 키와 값이 저장된 Map.Entry를 저장한다는 점이다.  
TreeMap에 객체를 저장하면 자동으로 정렬되는데,  
기본적으로 부모 키값과 비교하여  
키 값이 낮은 것은 왼쪽 자식 노드에, 키 값이 높은 것은 오른쪽 자식 노드에 Map.Entry 객체를 저장한다.  

<br/>

```java
TreeMap<K,V> treeMap = new TreeMap<K,V>();
TreeMap<String, Integer> treeMap = new TreeMap<>();
```

<br/>
<br/>

# TreeMap이 가지고 있는 검색 관련 메소드

---

<br/>

|리턴 타입  | 	메소드    | 설명                                                                              |
|---|---------|---------------------------------------------------------------------------------|
|Map.Entry<K,V>|firstEntry()| 제일 낮은 Map.Entry를 리턴                                                             |
|Map.Entry<K,V>|lastEntry()| 제일 높은 Map.Entry를 리턴                                                             |
|Map.Entry<K,V>|lowerEntry(K key| 	주어진 키보다 바로 아래 Map.Entry를 리턴                                                    |
|Map.Entry<K,V>|higherEntry(K key)| 	주어진 키보다 바로 위 Map.Entry를 리턴                                                     |
|Map.Entry<K,V>|floorEntry(K key)| 	주어진 키와 동등한 키가 있으면 해당 Map.Entry를 리턴, <br/>만약 없다면 주어진 키의 바로 아래의 키의 Map.Entry를 리턴 |
|Map.Entry<K,V>|ceilingEntry(K key)| 	주어진 키와 동등한 키가 있으면 Map.Entry를 리턴, <br/> 만약 없다면 주어진 키의 바로 위의 키의 Map.Entry를 리턴    |
|Map.Entry<K,V>|pollFirstEntry()	|제일 낮은 Map.Entry를 꺼내오고 컬렉션에서 제거함|
|Map.Entry<K,V>|pollLastEntry()|제일 높은 Map.Entry를 꺼내오고 컬렉션에서 제거함|

<br/>
<br/>

# TreeMap이 가지고 있는 정렬 관련 메소드

---

<br/>

| 리턴 타입             | 	메소드    | 설명                                                                              |
|-------------------|---------|---------------------------------------------------------------------------------|
| NavigableSet<K>   |	descendingKeySet()	|내림차순으로 정렬된 키의 NavigableSet을 리턴|
| NavigableMap<K,V> |	descendingMap()|	내림차순으로 정렬된 Map.Entry의 NavigableMap을 반환|

<br/>

```java
NavigableMap<K,V> descendingMap = treeMap.descendingMap(); //내림차순
NavigableMap<K,V> ascendingMap = descendingMap.descendingMap(); //오름차순
```

<br/>

| 리턴 타입             | 	메소드    | 설명                                                                                                         |
|-------------------|---------|------------------------------------------------------------------------------------------------------------|
|NavigableMap<K,V>|headMap(K toKey, boolean inclusive)	| 주어진 키보다 낮은 키의 Map.Entry들을 NavigableMap으로 리턴.<br/> 주어진 키의 Map.Entry의 포함 여부는 두번째 매개값에 따라 달라짐.                |
|NavigableMap<K,V>|tailMap(K fromKey, boolean inclusive)	| 주어진 키보다 높은 키들의 NavigableMap으로 리턴.<br/> 주어진 키의 Map.Entry의 포함 여부는 두번째 매개값에 따라 달라진다.                          |
|NavigableMap<K,V>|subMap(K fromKey, boolean fromInclusive, K toKey, boolean toInclusive)| 	시작과 끝으로 주어진 키 사이의 키들의 Map.Entry을 NavigableMap으로 리턴. <br/>시작과 끝 키의 Map.Entry 포함여부는 두번째, 네 번째 매개값에 따라 달라진다. |

<br/>
<br/>

# Comparable 과 Comparator

---

TreeSet 객체와 TreeMap의 키는 저장과 동시에 자동 오름차순으로 정렬되는데,   
숫자(Integer,Double)타입일 경우에는 값으로 정렬하고, 문자열(String)일 경우에는 유니코드로 정렬한다.  

<br/>

TreeSet과 TreeMap은 정렬을 위해 java.lang.Comparable을 구현한 객체를 요구하는데,  
Integer, Double, String은 모두 Comparable 인터페이스를 구현하고 있다.  
사용자 정의 클래스도 Comparable을 구현한다면 자동 정렬이 가능하다.  
Comparable에는 compareTo()메소드가 정의되어 있기 때문에  
사용자 정의 클래스에서는 이 메소드를 오버라이딩(재정의)하여 다음과 같이 리턴 값을 만들어야 한다.  

<br/>

|리턴 타입|메소드|설명                                                                  |
|---|---|-----------------------------|
|int	|compareTo(To)| 	주어진 객체와 같으면 0을 리턴<br/>주어진 객체보다 적으면 음수를 리턴<br/>주어진 객체보다 크면 양수를 리턴<br/> 오름차순, 내림차순 다 가능 |

<br/>
<br/>

{: .prompt-warning }
> TreeSet의 객체와 TreeMap의 키가 Comparable을 구현하고 있지 않을 경우에는  
> 저장하는 순간 ClassCastException이 발생하므로 주의하자.  

---

(참고)

- [[Java] HashSet, HashMap, TreeSet, TreeMap 정리](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=eguswhd&logNo=221909757781)
- [[이것이자바다] chapter 15. 컬렉션 - 검색 기능을 강화시킨 컬렉션 TreeSet, TreeMap](https://colinch4.github.io/2021-06-11/Collection_4/)

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>

<!--

❤️면접예상질문 ❤️

-->

