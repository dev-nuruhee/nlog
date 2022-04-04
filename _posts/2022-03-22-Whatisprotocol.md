---
title: Network - 프로토콜의 종류와 특징
published: true
---

## 프로토콜(Protocol)이란?
프로토콜은 다른 시스템 및 기기간 데이터 교환을 원활히 하기 위한 표준화된 통신 규약이다.

우리는 인터넷을 통해 많은 나라 사람들과 통신할 수 있다. <br>
이러한 통신을 하기 위해선 일종의 규칙이 지켜져야 서로 통신할 수 있을 것이 아닌가? <br>
**예를 들어** 미국인 친구와 한국인인 내가 만났다. <br>
근데 우리는 스페인에서 만났는데 어떤 언어를 사용할지 서로 정해야 의사 소통을 할 수 있다. <br>
이러한 어떤 언어를 사용한다는 것이 바로 **프로토콜**이다. <br>
여기서 말하는 언어는 **규약**이라 하고 이 규약 종류에 따라 어떤 프로토콜을 사용할지 정한다.

## 프로토콜의 구성
프로토콜은 구문(Syntax), 의미(Semantic), 타이밍(Timing)으로 구성된다. <br>
구문(Syntax)은 데이터를 어떻게 구성할건지, 구체적으로 어떻게 코딩할건지, 신호 레벨은 어떻게 할 것인지에 대한 형식을 규정한다. <br>
의미(Semantic)는 구성된 데이터들을 어떻게 제어할건지? 이 데이터가 에러가 나면 어떻게 처리할 것인지에 대한 정보를 포함한다. <br>
타이밍(Timing)은 통신이 이루어질 때, 데이터를 주고 받을 속도를 조절하거나 데이터 통신 순서 관리를 위한 기법이 포함된다. <br>

프로토콜 용도에 따라 많은 프로토콜들이 존재하는데 이건 구글링하여 찾은 이미지로 대체
![image](https://user-images.githubusercontent.com/54430432/159454197-d1257d7a-c080-4852-bba1-b23d68efe6ec.png)  
출처 : https://helloworld-88.tistory.com/146

## 1. TCP(Transmission Control Protocol)
네트워크 망에 연결된 컴퓨터의 프로그램 간 데이터를 순서대로 에러없이 교환할 수 있게 하는 프로토콜
제어의 역할이 강함<br>
특징으로는 첫번째로 **연결 지향 프로토콜**(Connection Oriented Protocol)이 있다.
연결 지향 프로토콜은 물리적으로 전용회선이 연결되어 있는 것처럼 가상의 연결통로(가상회선)를 설정하여 통신하는 방식
이러한 가상회선을 통해 통신할 때 데이터의 전송 순서를 제어한다. 
데이터 전송방식은 스트림(데이터를 임의의 크기로 나누어 연속해서 전송) 기반의 전송방식을 사용한다.<br>
두번째로는 **신뢰할 수 있는 프로토콜**(Reliable Protocol)이 있다. <br>
상대방이 수신 가능한 크기(Window Size) 내에서 데이터를 연속해서 전송하는 방식으로 매 세그먼트(Segmant, 프로그램 내 정의 되어 있는 특정영역) 전송 시마다 수신 확인 응답(ACK)을 수신한 후 전송하게 된다.<br>
전송하게 되면 왕복시간(RTT)이 길 경우 단위 시간당 데이터 전송 효율이 매우 떨어져 상대방이 받을 수 있는 범위 내에서 연속적으로 전송한다. <br>
데이터 오류나 누락없이 안전한 전송을 보장하고 이러한 현상들이 발생할 시 재전송을 수행하여 이런 현상을 보정한다. <br>
데이터의 손실 발생유무로 전송량을 조절한다. 전송 데이터 누락이 발생하면 네트워크가 혼잡한 것으로 판단하여 전송량을 조절한다.<br>

***TCP의 구조*** <br>
TCP는 기본적으로 Header와 Data로 구성된다.
![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile26.uf.tistory.com%2Fimage%2F99D7CE335BD7B0FF1C29FE) <br>
출처 : https://itragdoll.tistory.com/57

1. 출발지 포트 번호(Source Port / 16bits)
2. 목적지 포트 번호(Destination Port / 16bits)
3. 송신 데이터 순서 번호(Sequence Number / 32bits)
4. 다음 전송 순서 번호 (Acknowledgment Number / 32bits)
5. 헤더 길이 (HLEN / 4bits)
6. 예약 (Reserved / 4bits)
7. 제어 플래그 (Control Flags / 6bits)
- URG(Urgent pointer is valid) : 긴급 데이터 설정
- ACK(Acknowledgment is valid) : 수신 확인 응답(ACK) 설정
- PSH(Request for push) : 송수신 버퍼에 있는 데이터를 즉시 처리
- RST(Reset the connection) : 연결 중단(강제 종료)
- SYN(Synchronize sequence numbers) : 연결 설정
- FIN(Terminate the connection) : 연결 종료 (정상 종료)
8. 수신 가능 사이즈 (Window Size / 16bits)
9. 헤더를 포함한 전체 세그먼트에 대한 오류 검사 필드 (Checksum / 16bits)
10. 세그먼트가 긴급 데이터(URG 플래그)를 포함하고 있는 경우 사용되는 필드 (Urgent Pointer / 16bits)

***연결 과정***

![image](https://user-images.githubusercontent.com/14002238/115411131-2d788300-a22e-11eb-8557-0eb3e42d1096.png)
출처 : https://dongwooklee96.github.io/post/2021/04/20/tcp-%ED%86%B5%EC%8B%A0%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90....html

1. 클라이언트가 서버에 연결설정(SYN)을 전송한다. <br>클라이언트는 세그먼트의 시퀀스 번호를 임의의 값으로 설정.
2. 서버는 응답으로 SYN ACK를 응답. 수신된 세그먼트의 번호보다 큰 숫자로 설정됨
3. 클라이언트가 다시 서버에 수신 확인 응답(ACK) 를 보낸다.

이것을 3 Way Handshake라고 한다.

***연결 해제 과정***

![image](https://user-images.githubusercontent.com/14002238/115411888-d58e4c00-a22e-11eb-82d0-c47393198d7f.png)
출처 : https://dongwooklee96.github.io/post/2021/04/20/tcp-%ED%86%B5%EC%8B%A0%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90....html

1. 클라이언트가 연결 종료(FIN)를 전송한다.
2. 서버는 수신 확인 응답(ACK)을 보내고, 연결 종료(FIN)를 한다.
3. 클라이언트는 다시 수신 확인 응답(ACK)을 보내 과정을 마무리한다.

이것을 4 way Handshake라고 한다.

## 2. IP(Internet Protocol)
네트워크 주소와 호스트 주소의 정의에 의한 네트워크의 논리적 관리
초기 컴퓨터의 통신 방식은 회선 교환을 통해 이루어졌다.
상호 연결이 위해 전용 회선 또는 채널이 필요 했고, 통신하는 동안은 독점하고 있기 때문에 효율적으로 사용하지 못했다.
이러한 단점을 해결하기 위해 패킷 교환 방식으로 바뀌었다.

***패킷 교환 방식이 뭔데?***
작은 블록의 패킷으로 데이터를 전송하며 데이터를 전송하는 동안만 네트워크 자원을 사용하도록 하는 방법을 말한다. 정보 전달의 단위인 패킷은 여러 통신 지점(Node)을 연결하는 데이터 연결 상의 모든 노드들 사이에 개별적으로 경로가 제어된다. 이 방식은 통신 기간 동안 독점적인 사용을 위해 두 통신 노드 사이를 연결하는 회선 교환 방식과는 달리 짤막한 데이터 트래픽에 적합하다.

![image](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f6/Packet_Switching.gif/350px-Packet_Switching.gif)

하나의 파일은 작은 크기의 데이터들로 쪼개진다. <br>
쪼개진 데이터들은 발신지, 목적지 주수 정보를 추가하게 되면 하나의 단일한 패킷이 된다. <br>
이런 패킷들의 나열은 차레로 목적지까지 보내지고 패킷 나열을 다시 원본 파일로 재구성하는 작업이 이루어진다. <br>
패킷 단위로 나누기 때문에 회선 효율성이 좋고 트래픽에 따라 요청을 차단하거나 Store-and-Forward 방식을 사용하기 때문에 데이터 들어오는 속도와 나가는 속도를 맞 출 필요가 없다. <br>
Store-and-Forwart(축적교환방식)은 송수신 상호간에 직접적인 접속경로(회선 점유)를 만들지 않고
통신 정보를 중간 노드(스위치, 라우터 등) 등의 기억 매체를 활용하여 경유하게 됩니다.
이에 따라 중계 루트가 처음부터 정해지지 않고 구간별로 중계 루트가 변하는 형태로 상대방에게 전송 됩니다.
그렇기 때문에 전송 지연이 줄어들고 통신 안정성이 늘어난다. <br>

https://media.vlpt.us/post-images/doondoony/5b36e020-3dc7-11e9-8503-2572238e9a09/KakaoTalkPhoto2019-03-04-00-15-34.png
출처 : https://velog.io/@doondoony/ip101

여기서 Internet Protocol은 호스트간의 통신만을 담당한다.
그렇기 때문에 데이터를 보낼 때 받는 사람이 제대로 있는건지(연결), 받는 데이터가 맞는지(신뢰성) 관해서는 고려하지 않는다.

## 3. TCP/IP(Transmission Control Protocol/Internet Protocol)
인터넷 프로토콜 중 가장 중요한 역할을 하는 TCP와 IP의 합성어로 인터넷 동작의 중심이 되는 통신규약이다.
데이터 흐름 관리, 데이터의 정확성을 확인하는게 TCP의 역할이고 패킷을 목적지까지 전송하는 것이 IP의 특징!
IP는 데이터를 한 장소에서 다른 장소로 정확하게 옮겨주고 TCP는 전체 데이터가 잘 전송될 수 있도록 데이터 흐름을 조절한다.
- 응용계층 : 사용자 응용 프로그램으로부터 요청을 받아 적절한 메세지로 변환하고 하위 계층으로 전달
- 트랜스포트 계층 : IP에 의해 전달되는 패킷의 오류 검사 및 재전송 요구 등 제어를 담당 (TCP, UDP 두 종류의 프로토콜을 사용)

## 4. HTTP(Hyper Text Transfer Protocol)
WWW는 문서 기술언어인 **HTML**과 문서 전송 프로토콜 **HTTP** 문서의 주소를 지정하는 **URL**로 구성되었다. <br>
클라이언트의 요청 메세지에 대해 서버가 응답 메세지로 회신하는 형식 Default 서비스 PORT는 80번!

***요청 메세지 형식 예시***
```
GET /americano http/1.14  >>> 요청문
Host: starbucks.com        >>> 헤더
<공백 한 줄>
```

![image](https://user-images.githubusercontent.com/54430432/159454364-9625ddfe-1e22-4dbb-b032-f2def93f9583.png) <br>  
이미지 출처 : https://velog.io/@bining/%ED%81%B4%EB%9D%BC%EC%9D%B4%EC%96%B8%ED%8A%B8-%EC%84%9C%EB%B2%84-%ED%86%B5%EC%8B%A0-HTTP

의미는 HTTP서버 uu.ac.kr의 최상위 디렉토리 밑에 있는 index.php 파일의 전송 요청(GET)이다.
**HTTP 요청 메세지는 BODY가 없다**

***응답 메세지 예시***
```
HTTP/1.1 200 OK                           >>> 상태문
Date: Thu, 12 Feb 2009 06:29:38 GMT       >>> 헤더
Server: Apache/1.3.29 (Unix) PHP/4.3.4RC3 >>> 헤더
X-Powered-By: PHP/4.3.4RC3                >>> 헤더
Transfer-Encoding: chunked                >>> 헤더
Content-Type: text/HTML                   >>> 헤더
<공백 한 줄>

<HTML>                                    >>> 바디
<HEAD>
<TITLE> 타이틀 <TITLE>
...
```

의미는 상태문의 HTTP/1.1은 HTTP버전 200은 상태코드 OK는 상태이름!

기본적으로 요청(Request)의 종류가 9가지 정도가 있다.

- GET : 리소스 조회
- POST : 요청 데이터 처리, 주로 데이터 등록에 사용
- PUT : 리소스를 대체, 해당 리소스가 없으면 생성
- PATCH : 리소스를 일부만 변경
- DELETE : 리소스 삭제
- HEAD: GET과 동일하지만 메시지 부분을 제외하고, 상태 줄과 헤더만 반환
- OPTIONS: 대상 리소스에 대한 통신 가능 옵션을 설명(주로 CORS에서 사용)
- CONNECT: 대상 자원으로 식별되는 서버에 대한 터널을 설정
- TRACE: 대상 리소스에 대한 경로를 따라 메시지 루프백 테스트를 수행

Header의 종류도 3가지로 분류된다.
- General Header : 요청과 응답 모두에 적용되지만 바디와는 전혀 관련이 없는 헤더 
- Request Header : Petch될 리소스나 클라이언트 자체에 대한 자세한 정보를 포함하는 헤더 (클라이언트가 요청의 헤더)
- Response Header : 위치 또는 서버 자체 정보와 같이 응답에 대한 부가적인 정보 (서버의 응답의 헤더) 
- Entity header : 컨텐츠 길이나 MIME 타입과 같이 바디에 대한 자세한 정보를 포함하는 헤더

***General Header의 종류***
1. Date
```
Date: (day-name), (day) (month) (year) (hour):(minute):(econd) GMT
> Date: Wed, 21 Oct 2015 07:28:00 GMT
```
2. Connection
```
close, Keep-Alive가 있다.
-- close는 메세지 교환 후 TCP 연결 종료
-- Keep-Alive는 메세지 교환 후 TCP 연결 유지
> Connection: close
> Connection: Keep-Alive
```

***Request Header의 종류***
1. Host
```
요청하는 자의 호스트명, 포트 번호를 포함하고 있다.
> Host: nuruhee.mozilla.org
```
2. User-Agent
```
요청자의 소프트웨어 정보를 표현한다.
-- 소프트웨어 정보 : os, 브라우저, 기타 버전 정보
> User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:50.0) Gecko/20100101 Firefox/50.0
```
3. Accept
```
요청자가 원하는 미디어의 타입 및 우선순위를 표현한다.
Accept는 부속 속성이 더 있다.

Accept-Language : 사용자가 원하는 언어셋이다.
Accept-Encodig : 사용자가 원하는 인코딩 방식이다.

Accept: application/json, text/plain, */*
-> json > text > all type 순으로 받는다는 표현이다.
Accept-Language: en-US,en;q=0.5
-> 언어는 en이라는 표현이다. q는 가중치다.
Accept-Encoding: gzip, deflate, br
-> gzip, deflate, br(Brotli) 등등의 압축 포맷을 받는다는 표현이다.
```

4. cookie
```
서버에 의해서 이전에 저장된 쿠키를 포함시키는 속성이다.

- 예시
cookie: aaa=3LEMQRTO6EBF4; page_uid=bbb123p0YihsshvyCBRssssstWG-3033307; nx_ssl=100; nid_inf=333333333;NID_AUT=PSS11Z0wmL63LVUNoGF2ft123123123123/AomAn5zPT6Ni2uGyyuWIfp9hb; NID_JKL=TNg7Y994769rvA+5dcCHhdB7TBdl12345676+nQdCM=; AD_SHP_BID=9;spage_uid=hRDT1233455
```

5. Referer
```
Referer 요청 헤더는 현재 요청을 보낸 페이지의 절대 혹은 부분 주소를 포함한다.

두 가지의 속성을 더 가지고 있다.

referrer-policy : 이 헤더는 요청과 함께 얼마나 많은 레퍼럴 정보를 포함하는지 알려준다.

referer-after : 응답 헤더에 속하는 것인데, 다음에 올 요청이 이루어지기 전에 사용자가 대기해야 하는 시간을 가르킨다.

- 예시
referer:https://search.shopping.naver.com/search/allquery=%EA%B3%BC%EC%9E%90&cat_id=&frm=NVSHATC
```

***Response Header의 종류***
1. Server : 서버 소프트웨어의 정보를 표현한다.
2. content-encoding : 응답하는 내용의 인코딩 포맷을 표현한다.
3. content-type: 응답하는 내용의 타입과 문자 포맷을 표현한다.
4. cache-control : 캐시 관리에 대한 정보를 표현한다.
```
   cache-control :
   no-cache(서버측에 캐시를 사용해도 되는지 확인),
   no-store(캐싱x),
   must-revalidate(만료 캐시만 서버측에 확인),
   public(중개 서버에 저장 가능)/private(사용자 브라우저에만 등록),
   max-age(캐시 유효기간)
```
5. date : 응답 메세지가 생성된 시간을 표현한다.
6. vary : 캐시된 응답을 향후의 응답에 사용할 기준을 표현한다.
```
    Vary: User-Agent
```
   이렇게 설정되어 있으면, 모바일 유저에게 데스크탑 유저를 위한 캐시 컨텐츠가 제공되지 않게 할 수 있다.

7. Set-Cookie : 서버에서 사용자에게 세션 쿠키 정보를 전달한다.
8. Age : max-age내에서 캐시가 얼마나 지났는지 초 단위로 표현한다.









