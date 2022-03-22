---
title: [Network] 프로토콜과 HTTP 그리고 HTTPS까지
published: true
---

우리는 인터넷을 통해 많은 나라 사람들과 통신할 수 있다.
이러한 통신을 하기 위해선 일종의 규칙이 지켜져야 서로 통신할 수 있을 것이 아닌가?
예를 들어 미국인 친구와 한국인인 내가 만났다.
근데 우리는 스페인에서 만났는데 어떤 언어를 쓸지 정해야 소통이 될 것이 아닌가..
이러한 어떤 언어를 사용한다는 것이 바로 프로토콜이다.
여기서 말하는 언어는 **규약**이라 하고 이 규약 종류에 따라 어떤 프로토콜을 사용할지 정한다.

프로토콜 용도에 따라 많은 프로토콜들이 존재하는데 이건 구글링하여 찾은 이미지로 대체
![image](https://user-images.githubusercontent.com/54430432/159454197-d1257d7a-c080-4852-bba1-b23d68efe6ec.png)  
출처 : https://helloworld-88.tistory.com/146

이 많은 프로토콜 중 이번 글에서는 HTTP가 나온 배경과 HTTPS와의 차이점을 상세히 알아보겠다.

일단 HTTP는 Hyper Text Transfer Protocol의 줄임말이다.
그 유명한 WWW를 만든 팀버너에 의해서 제안되었다고 한다.
WWW는 문서 기술언어인 **HTML**과 문서 전송 프로토콜 **HTTP** 문서의 주소를 지정하는 **URL**로 구성되었다.

HTTP로 인터넷을 사용하기 이전에 윈도우 프로그램에선 **TCP/IP** 프로토콜을 사용하였는데, WWW에선 왜 HTTP를 사용할까?
그 이유는 TCP/IP는 상태성(연결된 상태인지 아닌지)을 가지고 있고 UDP에선 비연결성(연결절차 무필요)을 가지고 있는데 이러한 장점들을 가지기 위해 HTTP라는 프로토콜로 재설계 한 것이다.

즉 HTTP요청은 클라이언트의 상태를 알 필요가 없고, 요청에 대한 응답이 끝나면 연결을 끝내면 되는 장점을 갖게 된 것이다.

API에 맞게 요청을 하면 서버에서는 응답을 주는 형태

![image](https://user-images.githubusercontent.com/54430432/159454364-9625ddfe-1e22-4dbb-b032-f2def93f9583.png)  
출처 : https://velog.io/@bining/%ED%81%B4%EB%9D%BC%EC%9D%B4%EC%96%B8%ED%8A%B8-%EC%84%9C%EB%B2%84-%ED%86%B5%EC%8B%A0-HTTP

그렇다면 마지막으로 HTTP와 HTTPS의 차이점은?

HTTPS는 Hyper Text Transfer Protocol Secure의 줄임말이다.
HTTP의 클라이언트가 서버로 요청을 보내고 응답을 받을 때, 이 응답이 암호화 되지 않기 때문에 데이터의 유실 위험이 있다.
그렇게 암호화를 위해 나온 것이 HTTPS이다.
HTTPS는 SSL(보안 소켓 계층)을 사용함으로써, 해당 문제를 해결하였다.
SSL인증서가 없으면 서버의 응답을 볼 수 없는 구조로 바뀐 것이다!




