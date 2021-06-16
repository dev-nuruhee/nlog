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

###출처 : https://dojang.io/mod/page/view.php?id=293 (코딩 도장)

<br>

이러한 내용들은 기본이지만, List와 ArrayList, Array의 3가지 차이점을 비교해볼까?


###Array VS ArrayList VS List 
1. **Array**는 기본적으로 크기를 정해놔야함
1. **ArrayList는** 크기를 늘릴 수 있음
1. **ArrayList는** 클래스임
1. **List**는 인터페이스임


### [](#header-3)Header 3
```java
ArrayList<Object> list = new ArrayList<>();
List<Object> list = new ArrayList<>();  
```
