---
banner: "![[Title01.png]]"
tags:
---
>**웹과 HTTP을 이해하기 위한 정리 글임.**
>이 프로젝트는 아주 기본적인 HTTP과 Web Server의 기본적인 지식을 쌓고, 심화 과정인 WEB Assemble까지 이어갈 예정이며, 해당 글은 HTTP과 Web Server의 기본적인 지식을 정리 한 것으로 이론 부분에서 집중하여 읽으면 될 것 같습니다.

<br/>


# WEB이란 무엇일까?

먼저 웹을 본다면 먼저 보이는 URL[^1]이 존재한다.
```url
https://www.twich.tv/handongsuk
```
해당 URL[^1]을 보면 ```https```도 있고, ```www.twich.tv```도 있으며, 뒤에 handongsuk이라는 의미를 알 수 없는 변수도 오는 것을 볼 수 있다.
이러한 위치마다 각자의 역할과 용어의 내용을 어떤 것일까? 라는 궁금증이 생기지 않는가? 이번 정리를 통해서 이론적인 부분으로 https와 www가 무엇인지, 우리가 특정 사이트에 진입할 때에 외워야 되는 URL에 대해서 정리할 예정이다.

## HTTP의 이해
- - -
HTTP[^2]은 수십억 개의 JPEG 이미지, HTML Page, Text 파일, MPEG 동영상, WAV 음성 파일과 같은 웹 Resource를 빠르고, 간편하고, 정확하게 필요한 사람들에게 제공할 수 있도록 하는 Protocol[^3]이다. 이처럼 HTTP는 신뢰성 있는 데이터 전송 Protocol을 사용하기 때문에 Data의 분실이나 손상되는 우려가 없다.
이에 개발자는 Data의 결함이나 약점에 대한 걱정이 없이 Web이나 App의 고유 기능을 개발하는 데에 집중할 수 있다.

### Web Client & Server

![[Pasted image 20230927164745.png]]
[[그림 1-1] Web Client & Server](https://hackernoon.com/http-made-easy-understanding-the-web-client-server-communication-yz783vg3)

Web Content는 Web Server에 존재한다. 그러면 어떻게 Client가 Web Content를 얻을 수 있을까? 
위의 **그림 1-1**을 참고하면, Client는 해당 Content에 접근 할 때에 Web Server에 HTTP Request를 보내게 되고 해당 Request에 대한 Response를 만들어서 Server는 Client에 Content를 제공해준다. 이것이 가장 기본적인 Web 통신의 요소이다. 

이때 활용하는 것이 URL인데 이것이 Web Browser에서 Server에 HTTP 객체를 요청하고 Client의 화면에 보여준 결과물이다.
```url
https://www.twich.tv/handongsuk
```
예시로 필자가 자주 보는 방송의 링크를 예시로 설명을 하도록 하겠다.

해당 URL을 보면 HTTP 요청을 'www.twich.tv' Server로 보낸다. Server는 요청 받은 객체 'handongsuk'을 찾고 그것의 정보들을 Client에 응답하는 것이다.
그러면 객체가 될 수 있는 Resource에 대해서 알아보도록 하겠다.

#### Resource

Web Server는 Web Resource를 관리하고 제공하는 역할을 한다. 우리가 볼 수 있는 가장 단순한 Resource에는 Web Server File System의 정적 파일이다. 
정적 파일은 Text 파일이나, HTML 파일 그리고 이미지 파일 등등 그 외 모든 종류의 파일을 말한다. 

하지만 Web Resource는 반드시 정적 파일일 필요는 없다. 요청에 따라서 Content를 생성하는 Program이 될 수도 있는 것이다. 예를 들어 사용자가 영상을 요청하여, 카메라에서 라이브 영상을 가져와 보여주거나, 실시간 주식 거래, 온라인 쇼핑몰에서 선물 구입하는 등의 활동을 할 수 있도록 하는 일을 말한다.
_"인터넷 검색 엔진도 Resource이다."_

그러면 Resource를 담당하는 media의 type에 대해서 알아보도록 하자.

#### Media Type

인터넷은 수천가지의 Data Type을 다루기 때문에 HTTP는 웹에서 전송되는 객체 각각에 신중하게 MIME[^4] Type이라는 Data Fomat Label을 붙인다.
해당 타입은 원래 각기 다른 전자메일 시스템에서 메시지가 오갈 때에 타입이 각기 다른 문제점을 해결하기 위해 설계된 타입이다. 이메일에서 잘 동작을 하는 것을 확인하고 HTTP[^2]에서 멀티미디어 콘텐츠를 기술하고 라벨을 붙이기 위해 채택하였다.

웹 서버는 모든 HTTP[^2] 객체 데이터에 MIME Type을 붙인다.
![[Pasted image 20231010155548.png]]

해당 그림을 참고하면, <Content-type: image/jpeg> 가 적혀있는 것을 볼 수 있다.
즉, 서버로부터 객체를 돌려 받을 때에, 다룰 수 있는 객체인지 MIME Type을 통해 확인하고, 이를 돌려주는 것을 확인 할 수 있다.

MIME Type은 `/ (사선)`으로 구분된 주 타입(primary object type)과 부 타입(specific subtype)으로 이뤄진 문자열 라벨로 종류는 이렇게 되어 있다.

| 종류        | 라벨       |
| ----------- | ---------- |
| HTML        | text/html  |
| plain ASCII | test/plain |
| JPEG Image  | image/jpeg |
| GIF         | image/gif  |

이 외에도 수백 가지의 MIME Type이 존재하니 전체적인 타입은 인터넷을 참고하여 알아보면 될 것 같다.

이렇게 우리는 Web을 이루는 컨텐츠의 주 요소가 되는 Resource와 그들의 Type을 나누는 MIME에 대해서 알아보았다. 그렇다면, 이러한 컨텐츠에 접근을 하기 위한 경로인 URL은 대체 무엇이고, 어떠한 규약이 존재하는지 알아보도록 하자.

#### URI
웹 서버에서 각각의 Resource는 이름이 존재하기 때문에 Client는 관심이 있는 컨텐츠에 접근하기 위해 Resource를 지목해야 되는데,
이를 위해 통합 자원 식별자(Uniform Resource Identifier) 즉, URI이라고 부르는 것을 이용할 수 있다.

```url
https://www.example.com/exampleTest/example.html?example=123
```
해당 예시를 보면, example.html이라는 컨텐츠에 접근하기 위해  URL에서 HTTP Protocol에서 어떻게 해석 되어졌는지 보여주는 부분이다.
하지만, 아까의 예시에선 URL이라 하였지만, 지금은 URI라고 칭하고 있다. 대체 URL은 무엇이고 URI와 차이점은 무엇인지 설명하도록 하겠다.

![[Pasted image 20231010163452.png]]
URL은 URI에 속해 있으며, URI가 2가지로 나눠진다. URN과 URL이 이에 속한다.

##### URI
URI는 어떤 형식이 있다기 보단 특정 자원을 식별하는 문자열의 나열을 의미한다. 즉, URI중 URL이라는 하위 개념을 만들고 특별히 어떤 표준에 맞춰서 자원을 식별하는 문자열이라는 것이다.

##### URL
URL은 Uniform Resource Locator의 약자로, 통합 자원 지시자라고 한다. 이 URL은 특정 서버에서 Resource의 위치 정보를 나타내는 부분이다.

URL은 3 부분으로 이뤄져있다.

Scheme : 리소스에 접근하기 위해 사용되는 Protocol을 서술하는 부분
( HTTP Protocol -> `http://`, HTTPS Protocol -> `https://`)

Location : 서버의 인터넷 주소를 서술하는 부분
Example : www.naver.com

Resource : 웹 서버의 Resource를 지정하는 부분
Example : /example/example1.html

```url
https://www.example.com/exampleTest/example.html?example=123
(Scheme) // ( Server Location ) / (Resource Location)
```

위의 예시를 가져와서 설명하면, 해당과 같다는 것을 볼 수 있다.

##### URN
URN은 Uniform Resource Name의 약자로, 콘텐츠를 이루는 하나의 Resource에 대해, 그 Resource의 위치에 영향 받지 않는 유일무이한 이름 역할을 담당한다.
즉, 해당 Resource를 여기저기 옮겨놔도 독립적인 URN은 문제 없이 동작한다.

##### URI랑 URL의 차이점이 뭐죠 대체?
이렇게만 듣는다면, 이게 뭔소리지? 예제 좀 보여줘요~ 라는 생각이나 말이 나올 수 있다.
이에 답을 주자면, URL과 URN은 URI의 종류이며, 모든 URL은 URI이며 모든 URN은 URI이다. 하지만, URL과 URN은 다르다.

쉽게 말하자면, URI는 규약이며, URL은 규약에 대한 형태를 말하는 것이다.
우리가 흔히 보는 URL
```url
https://www.example.com/exampleTest/example.html?example=123
```
이것이 바로 URI 규약 중 URL 규칙을 따르는 문자열이라는 것을 알면된다.

##### 그러면 URN은 뭐죠? 본 적이 없는 것 같은데
URN은 URL의 한계를 보완하기 위해 만들어졌지만, 아직 채택된 방식이 아니라 본 적은 없을 것이다.
```url
https://stonecat.tistory.com/19
```

만약 해당 URL이 존재한다고 가정해보자, 주소의 관리자가 해당 주소를 변경하고자 
```url
https://stonecat.tistory.com/example/19
```
위의 주소로 변경을 했을 경우 위의 주소를 검색한다면, 주소의 관리자가 의도한 데로 컨텐츠를 즐길 수 있을 것이다. 하지만, 이전의 주소는 접근 자체가 거부될 것이다. 지정한 것이 없다면, 아무것도 없기 때문이다.

즉, URL에서 Resource가 옮겨졌을 경우 기존의 URL을 더 이상 사용할 수 없기 때문에, 이러한 단점을 보완하기 위해 객체의 위치와 관련 없이 해당 객체에 이름을 부여하여 그 객체의 이름을 지정하면 위치에 관계없이 찾아서 갈 수 있도록 하는 방법이 URN이다.

*"결론적으로는 우리는 URI의 규약 내의 URL을 따르는 주소를 접하고 있다."*



## HTTP Message의 이해
- - -
우리는 지금까지 웹이 Client로 하여금 콘텐츠에 어떻게 접근을 해야 되고 필요한 Resource를 어떻게 받아내는 지에 대해 알아보았다. 그렇다면, Client와 Server간의 통신은 어떻게 이뤄지는지 궁금하지 않은가?

우리가 통신을 할 때에 Client와 Server는 콘텐츠에 필요한 Resource를 성공적으로 주고 받았는지 실패했다면 어떻게 구별하고, 자원이 필요 여부에 대한 부분을 어떻게 남기는 것인지 궁금할 것이다. 이에 웹은 Client와 Server간의 통신에 무리가 없게 진행될 수 있도록 HTTP Message를 만들어서 이를 통해 구분하고 있다.

그렇다면, HTTP Message에는 어떤 정보가 들어있고, 개발자는 이러한 정보를 통해서 어떻게 코드를 이끌어 낼 수 있는 지에 대해서 알아보도록 하겠다.


HTTP Message는 시작 줄, 헤더, 본문 이렇게 3 부분으로 나눠진다.

먼저, 시작 줄은 메시지의 첫 줄을 의미하며, 요청이라면 어떤 것을 해야 되는지 응답이라면, 어떤 일을 해야 되는지 작업을 명시하는 곳이다. 

| 경우     | Explanation                                                               | Example                        |
| -------- | ------------------------------------------------------------------------- | ------------------------------ |
| Request  | Get, Post, Delete 등, 요청 Method와 필요한 Resource 그리고 통신 버전 등.. | GET /test/example.txt HTTP/1.0 |
| Response | 통신에 대한 결과와 통신 버전 등..                                         | HTTP/1.0 200 OK                               |



#### Transaction
Client가 웹 Server와 Resource를 주고 받기 위해서 HTTP를 어떻게 사용하는지 이 HTTP Transaction을 통해서 알 수 있다.
Transaction은 매우 쉽게 말해서 거래 내역이라고 보면 된다. 

Transaction은 Request와 Response로 구성되어있으며, 해당 상호작용은 HTTP MSG라고 불리는 정형화된 데이터 덩어리를 이용하여 이뤄진다.
![[Pasted image 20231019143219.png]]

쉽게 말해서 우리가 웹 컨텐츠에 접근을 시작할 때부터 모든 자원을 받아올 때 까지 모두 트랜잭션의 과정이라고 할 수 있다.

해당 트랜잭션을 위한 HTTP MSG에는 출발지 IP, 목적지 IP, 등등 다양한 정보가 존재한다.
IP에 관련된 이야기나, TCP, UDP와 같은 프로토콜 계층은 후에 다시 설명을 부여하도록 하겠다.

이번은 우리가 HTTP MSG를 구분하는 방법과 어떤 내용이 들어가는 지에 대해서 자세히 알아보도록 하겠다.

#### Method
HTTP MSG를 통해서 트랜잭션을 형성하기도 하지만, Request의 종류를 구분하기 위해서 Method를 통해서 구분한다.
우리가 통신을 할 때에 흔히 쓰이는 메서드는 5개가 있다.

| HTTP Method | Ex                                                                |
| ----------- | ----------------------------------------------------------------- |
| GET         | Server에서 Client로 지정한 Resource를 보내라                      |
| PUT         | Client에서 Server로 보낸 Data를 지정한 이름의 Resourse로 저장하라 |
| DELETE      | 지정한 Resource를 Server에서 삭제하라                             |
| POST        | Client Data를 Server Gateway Application으로 보내라               |
| HEAD        | 지정한 Resource에 대한 Response에서 HTTP Header부분만 보내라      |

//3장 참고 후 추가

#### Status Code
모든 HTTP MSG가 성공적인 MSG를 보낼 수는 없다. 그렇기에 해당 Request가 올바르게 받아졌는지 확인하는 코드가 존재한다.

| HTTP Status Code | Ex                                              |
| ---------------- | ----------------------------------------------- |
| 200              | GOOD, Resource가 올바르게 반환됨                |
| 302              | 다시 보내라, 다른 곳에 가서 Resource를 가져가라 |
| 404              | 없음, Resource를 찾을 수 없다.                  |

각 Status  Code만 보내는 것이 아닌 상세한 사유 구절[^5]도 같이 보낸다.

//3장 참고 후 추가




[^1]: Uniform Resource Locator의 약자로 파일 식별자, 유일 자원 지시기 라고 불리우며, 네트워크 상에서 자원이 어디에 존재하는지 알려주기 위한 표현 규약임.
[^2]: HyperText Transfer Protocol의 약자로 World Wide Web의 토대이며, Hypertext Link를 사용하여 웹 페이지를 Load 하는 데에 사용된다.
[^3]: 복수개의 컴퓨터 사이나 중앙 컴퓨터와 단말기 사이에서 데이터 통신을 원활하게 하기 위해서  필요한 통신 규약을 말한다. 쉽게 말해 데이터의 표현 법이다.\
[^4]: Multipurpose Internet Mail Extensions의 약자
[^5]: Reason phrase라고 불리움, Document attached나 Success 등등 status code에 맞게 개발자가 넣은 간단한 문장.