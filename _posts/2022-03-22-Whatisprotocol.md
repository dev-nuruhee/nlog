---
title: [Network] 프로토콜의 종류와 특징
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

## 1. HTTP(Hyper Text Transfer Protocol)
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







