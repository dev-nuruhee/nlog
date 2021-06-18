---
title: 자료구조 
published: true
---

# [](#header-1)<자료구조>배열 (Array)

개발을 하는 사람중에 배열을 모르는 사람은 없을 것이다.<br>
정보성 글이기에 몇가지 특징과 우리가 알고 있어야할 필요 지식들을 적어보겠음 <br>
배열은 순차적으로 데이터를 저장하고 인덱스 번호로 접근함<br>
그렇기에 빠른 접근이 가능하지만, 데이터를 추가하거나 삭제에 있어 비교적 어려워. <br>

![배열](https://user-images.githubusercontent.com/54430432/122173266-9261f980-cebc-11eb-8a8d-9bb70dd92f3c.PNG)

### 출처 : https://dojang.io/mod/page/view.php?id=293 (코딩 도장)

<br>

이러한 내용들은 기본이지만, List와 ArrayList, Array의 3가지 차이점을 비교해볼까?


### Array VS ArrayList VS List 
1. **Array**는 기본적으로 크기를 정해놔야함, 삭제를 하더라도 빈공간으로 존재하기 때문에 GC(Garbage Collection)발생<br>
1. **ArrayList는** 크기를 늘릴 수 있음
1. **ArrayList는** 클래스임
1. **List**는 인터페이스임


### [](#header-3) 세가지를 보면?
```java
ArrayList<Object> list = new ArrayList<>();
List<Object> list = new ArrayList<>();  
List<Object> list = new LinkedList<>();

```

위 코드들을 읽어보면 List가 ArrayList와 LinkedList에 대해 더 큰 개념이라는걸 알 수 있다. <br>
결국 다형성을 위해서 저렇게 나뉘어서 쓰는 것인데, 여기서 인터페이스에 대한 명확한 개념을 알고 있어야 한다.
인터페이스는 모든 메서드가 추상 메서드이다. 하지만 이를 상속 받은 ArrayList나 LinkedList는 클래스 이기 때문에 new 연산자가 사용 가능한것 
더 나아가 탐색 속도에 따라 ArrayList나 LinkedList 둘 중 더 어떤게 적재적소에 사용할 것인지를 파악하는 것이 중요하다.
