---
title: JAVA - JAVA의 메모리구조와 Gabage Collection(GC)
published: true
---

개발을 하다보면 유효하지 않는 메모리들이 발생한다.
이러한 것들을 정리해주는게 Garbage Collection이라 한다.

그렇다면 JAVA는 메모리를 어떻게 사용하고 어떤 경우에서 Garbage Collection이 메모리를 정리 할까?
우선 Garbage Collection을 알기 이전에 우리는 JAVA의 메모리를 알 필요가 있다.

### JAVA 메모리 구조
JAVA로 작성된 프로그램들은 JVM을 통해서 실행된다.<br>
JVM을 통해 실행하기 위해선 JAVA가 Class파일로 컴파일 되어야 한다.<br> 
이러한 과정을 컴파일이라고 하고 JAVA는 byte코드로 변환하여 class파일로 바뀐다.<br>
JVM은 Class Loader를 통해 이 class파일을 가져오고 Runtime Data Area에 분배한다.<br>
Runtime Data Area에 분배된 byte코드들은 Execution Engine을 통해 실행된다.<br>
이 분배 영역(Runtime Data Area)중 Heap Area에 배정되고, 유효하지 않은 객체들을 정리해주는 것이 오늘 알아볼 **Garbage Collection**이다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FpjywN%2FbtqSduBXLIK%2F2QEL5c2nEJXRm0cyhvwxF1%2Fimg.png)
출처 : https://steady-coding.tistory.com/305

#### Runtime Data Area
- Method Area : 모든 쓰레드가 사용하는 메모리 영역, 클래스, 인터페이스, 메소드, 필드, Static 변수 등의 바이트 코드를 보관
- Heap Area : 모든 쓰레드가 공유하고, new 키워드로 만들어지는 객체와 배열이 생성되는 영역 -> Garbage Collector가 관리
- Stack Area : 매서드 호출시마다 각각의 스택 프레임을 생성하고 안에서 사용되는 값들을 임시 저장. 매서드가 끝나면 스택 프레임 삭제
- PC Register : 쓰레드가 실행될 때마다 생성되고 쓰레드에게 명령을 주는 주소를 기록
- Native Method Stack : 자바 외 네이티브 언어를 사용할 때 저장되는 공간

### Garbage Collection
우리가 개발할 때 아래와 같은 코드가 있다 예를 들자
```java
Nuruhee nr = new Nuruhee();
nr.setName = "이누리";
nr = new Nuruhee(); //Garbage Collection 발생
```
위와 같이 불필요한 부분들을 Garbage Collector는 정리하는데 어떻게 정리를 하는 것일까?

Garbage Collecor는 Heap영역을 정리하고 Heap영역에는 new 키워드로 만들어지는 객체와 배열이 생성된다고 했다. <br>
이러한 Heap영역은 기본적으로 전제 조건을 깔고 만들어졌는데, <br>
첫번째로는 **대부분의 객체는 금방 접근 불가능한 상태**가 되고 <br>
두번째로는 **오래된 객체에서 새로운 객체로의 참조는 아주 적게 된다**는 전제이다. <br>

***객체는 대부분 일시적이고 오랫동안 남아 있는 객체는 드물다***는 것이다.
이러한 이유로 Heap은 Young한 부분과 Old한 부분으로 나뉘었다.

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fva8qQ%2FbtqUSpSocbS%2FkxTvtnmrdhf4bnVPXth0UK%2Fimg.png)

출처 : https://mangkyu.tistory.com/118

대부분의 객체는 Young의 부분에 할당되고 Garbage Collection에 의해 정리되는데, Young 영역에서 발생한 정리를 Minor GC라고 부른다.<br>
Young 영역에서 접근 가능한 상태가 유지되면 Old 영역으로 넘어오게 된다. <br>
하지만 이 마저도 영원히 사용하는게 아니기 때문에 정리를 당하게 되는데, 이러한 것을 Major GC라 부른다.
Young의 영역보다 Old의 영역이 크지만, Garbage는 적게 발생한다.

간혹가다 Old영역에 있는 객체들이 Young 객체들을 참조하는 경우가 있는데, 이것을 대비해서 Old 영역에는 Card Table이 존재한다.
정리하기 위해서 모든 Old영역을 확인할 수 없기에 Card Table만 참조하여 GC의 대상인지 아닌지 판별하는 것이다.

Garbage Collection이 동작하는 방식은 2가지 방법이 있다.
1. Stop The World
2. Mark and Sweep

Stop The World는 말 그대로 세계를 멈추는 것이다. <br>
프로그램 입장에서 세계를 멈춘다는건 JVM이 멈추는 것과 같다. <br>
환경미화원이 청소를 하기 위해 시간을 멈추는 것과 같다고 생각하면 된다. <br>

멈춘 세계에서 환경미화원(GC)는 어떻게 버릴 대상을 판단할까? <br>
누군가가 사용하고 있는 중인지 확인하고(Mark) 사용하고 있지 않다면 해제해버린다.(Sweep)

