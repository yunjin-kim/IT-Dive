# HTTP

##  Reference 
- [모든 개발자를 위한 HTTP 웹 기본 지식](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/dashboard);

## IP (인터넷 프로토콜)
Internet Protocol

### 인터넷 프로토콜의 역할
- 지정한 IP 주소에 데이터 전달
- 패킷(Packet)이라는 통신 단위로 데이터 전달
  - 패킷에는 출발지 IP, 목적지 IP, 전송 데이터 등이 실린다

<img src='../img/packet.png' width='700'/>

클라이언트가 서버로 패킷을 전달할 때 여러 노드를 거쳐서 서버에 전달된다

<img src='../img/client_packet.png' width='700'/>


### IP 프로토콜의 한계
- 비연결성: 패킬을 받을 대상이 없거나 서비스 불능 상태여도 패킷을 전송한다
- 비신뢰성: 중간 노드에서 패킷이 사라지거나 패킷이 순서대로 오지 않는 문제
  - 패킷을 순서대로 보내더라도 거쳐가는 노드가 다르기 때문에 보낸 순서대로 오지 않을 수 있다
- 프로그램 구분: 같은 IP를 사용하는 서버에서 통신하는 애플리케이션이 둘 이상일 때 문제

이 문제의 해결책으로 TCP, UDP가 있다


## 인터넷 프로토콜 스택의 4계층
<img src='../img/protocol_stak.png' width='700'/>


## 프로토콜 계층
<img src='../img/protocol.png' width='700'/>


## TCP (전송 제어 프로토콜)
Transmission Control Protocol

TCP는 IP패킷에 TCP 세그먼트를 씌워운다
<img src='../img/tcp.png' width='700'/>

### TCP 특징
- 연결 지향: TCP 3 way handshake(가상 연결)
- 데이터 전달 보증
- 순서 보장: 패킷1, 2, 3을 보냈는데 패킷1, 3, 2 순서로 도착하면 패킷2부터 다시 보내라고 요청한다
- 신뢰할 수 있는 프로토콜
- 현재 대부분 TCP 사용

TCP 3 way handshake
<img src='../img/3handshake.png' width='700'/>


## UTP (사용자 데이터그램 프로토콜)
User Datagram Protocol

### TCP 특징
- 하얀 도화지에 비유(기능이 거의 없다)
- 연결 지향  TCP 3 way handshake X
- 데이터 전달 보증 X
- 순서 보장 X
- 단순하고 빠르다
- IP와 거의 같다. +PORT, +체크섬 정도만 추가
- 애플리케이션에서 추가 작업이 필요하다


## PORT

TCP/IP 패킷에는 출발지 IP, 출발지 PORT, 목적지 IP, 목적지 PORT, 전송 데이터 등이 들어 있다
PORT는 같은 IP 내에서 프로세스를 구분한다
<img src='../img/port.png' width='700'/>

PORT는 0 ~ 65535 사이에서 할당 가능하다
- 0 ~ 1023: 잘 알려진 포트, 사용하지 않는 것이 좋다
- FTP: 20, 21
- TELNET: 23
- HTTP: 80
- HTTPS: 443


## DNS (도메인 네임 시스템)
Domain Name System
- 전화번호부
- 도메인 명을 IP 주소로 변환

IP는 기억하기 어렵고 변경될 수 있기 때문에 DNS 시스템이 필요하다
<img src='../img/dns.png' width='700'/>


## URI (Uniform Resource Identifier)

- Uniform: 리소스를 식별하는 통일된 방식
- Resource: 자원, UIR로 식별할 수 있는 모든 것(제한 없다)
- Identifier: 다른 항목과 구분하는데 필요한 정보


### URL, URN

- URL: Locator, 리소스가 있는 위치를 지정
- URN: Name, 리소스에 이름을 부여
- 위치는 변할 수 있지만, 이름은 변하지 않는다
- URN 이름만으로 실제 리소스를 찾는 방법이 보편화 되지 않음
- URI, URL을 같은 의미라고 생각해도 무방

<img src='../img/uri.png' width='700'/>


## URL

scheme://[userinfo@]host[:port][/path][?query][#fragment]

https://www.google:443/search?q=hello&hi=ko
프로토콜  호스트명    포트번호  패스   쿼리 파라미터

### scheme
- 주로 프로토콜 사용
- 프로토콜: 어떤 방식으로 자원에 접근할 것인가 하는 약속
  - ex) http, https, ftp 등
- http는 80포트, https: 443 포트를 주소 사용, 포트는 생략 가능
- https는 http에 보안 추가한 것

### userinfo
- URL 에 사용자 정보를 포함해서 인증
- 거의 사용하지 않는다

### host
- 호스트명
- 도메인 명 또는 IP 주소를 직접 사용가능

### port
- 접속 포트
- 일반적으로 생략한다, 생략시 http는 80 https는 443

### path
- 리소스 경로, 계층적 구조
- ex) /home/profile
      /member/id=1

### quert
- key=value 형태
- ? 로 시작, & 로 추가 기능 ?keyA=valueA&keyB=valueB
- query parameter, query string 등으로 부른다, 웹서버에 제공하는 파리미터, 문자 형태

### fragment
- html 내부 북마크 등에 사용
- 서버에 전송하는 정보 아니다


## 웹 브라우저 요청 흐름
https://www.google:443/search?q=hello&hi=ko

1. HTTP 요청 메서지를 생성한다

GET /search?q=hello&hi=ko HTTP/1.1
HOST: www.google.com

2. SOCKET 라이브러리를 통해 전달
  - TCP/IP 연결
  - 데이터 전달

3. TCP/IP 패킷 생성, HTTP 메시지 포함

4. 웹 브라우저는 서버로 요청 패킷을 전달한다

5. 서버는 요청 패킷을 받고 응답 패킷을 전달한다

6. 웹 브라우저는 응답 패킷을 받고 HTML을 렌더링한다