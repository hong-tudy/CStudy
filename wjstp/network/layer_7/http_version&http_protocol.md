# 버전별 HTTP & HTTP 프로토콜 구조
HyperText Transfer Protocol. www에서 쓰이는 핵심 프로토콜로 문서의 전송을 위해 쓰인다. 

## 버전별 HTTP

### HTTP/0.9 (1991년)

- method도 get만 존재. http 헤더도 없고, html 파일만 전송 가능

### HTTP/1.0 (1996년)

- http header 개념 도입.
- 커넥션 하나 당 응답 하나만 처리 가능 → 통신 부하 발생
    - `연결수립 -> 동작 -> 연결해제` 과정 반복. html 문서 전송받으면 연결끊고, 다시 연결해서 데이터 전송

### HTTP/1.1 (1997년) : 가장 많이 사용중. 모든 것이 1.1 버전이 기반이다.

- **Persistent Connection 추가**
    - 지정한 timeout동안 커넥션을 닫지 않는 방법을 통해 커넥션의 사용성이 높아짐
- **Pipelining 추가**
    - 앞 요청의 응답을 기다리지 않고, 순차적인 여러 요청을 연속적으로 보내고, 그 순서에 맞춰 응답을 받는 방식
        
        → 하나의 요청 + 응답 이 순차적으로 처리되는 기존 방식을 개선
        
    - multiplexting (x) : 동시에 여러개의 요청을 처리해 응답으로 보내주는 것은 아님. 하나의 커넥션에 여러개의 요청이 들어있는 것
- **한계**
    - Head of Line blocking : 앞 요청의 응답이 너무 오래 걸리면 뒤 요청은 blocking 된다.
    - header 구조의 중복 : 연속된 요청의 헤더의 많은 중복 발생

### HTTP/2.0 (2015년) : HTTP 1.1의 성능 개선 및 확장

- 기존 http1.x 버전의 성능 향상에 초점을 맞춘 것으로, 대체가 아닌 확장이다.
- **HTTP 메시지 전송 방식의 전환**
    - 일반 텍스트 형식 → Binary Framing 계층을 추가 : 메시지를 프레임이라는 단위로 분할하며 추가적으로 바이너리로 인코딩. 전송속도 ⬆️ 오류 발생 가능성 ⬇️
- **Multiplexed Streams**
    - 하나의 커넥션 안에 여러개의 스트림을 가질 수 있게 되어 다중화가 가능해짐. 각 요청의 응답 순서가 의미가 없어지므로 HOL Blocking 문제가 자연스럽게 해결됨.
- **Stream Prioritization**
    - 리소스 간 우선순위를 설정하는 기능
- **Server Push**
    - 단일 클라이언트 요청에 여러 응답을 보낼 수 있는 특징을 통해 Server에서 클라이언트에 필요한 추가적인 리소스를 push 해주는 기능
- **Header Compression**
    - 기존 : 연속된 요청의 경우 많은 중복된 헤더의 전송으로 오버헤드가 많이 발생하였음
    - 개선
        - 요청과 응답의 헤더 메타데이터를 압축
            - 전송되는 헤더 필드를 static dynamic table로 서버에서 유지
            - 이전에 표시된 헤더를 제외한 필드를 허프만 인코딩해서 데이터 압축
- **한계**
    - 각 요청마다 Stream으로 구분해 병렬적으로 처리하지만, 결국 TCP고유의 HOL Blocking이 존재
        - 서로 다른 stream이 전송되고 있을 때, 하나의 stream에 유실이 발생하거나 문제가 생기면 다른 stream도 문제가 해결될때까지는 지연되는 현상이 발생
    - 이 문제를 해결하기 위해 HTTP3.0등장 (UDP 기반 전송 프로토콜)

### HTTP/3.0 (진행중)

- Google에서 개발한 UDP기반의 전송 프로토콜 (QUIC, Quick UDP Internet Connections)
- TCP의 3way handshake 과정을 최적화하는 것에 초점을 두고 개발

## HTTP 프로토콜의 구조

### 요청 프로토콜

- Request Line : 요청 타입 + 공백 + URI + 공백 + HTTP버전
    - `GET /produ/content.asp?code=scv-v310 HTTP/1.1`
    - 요청 타입
        - GET : 값을 가져올 때 사용 / URI에 전달 값 노출 / 길이 제한 o / 형식에 맞지 않으면 인코딩 필요
        - POST : 서버의 값이나 상태 변경시 사용 / HTTP BODY에 데이터 포함해서 전달 / 길이 제한 x
- Headers : 옵션들
- Body : 데이터를 요청할 때 보내는 추가적인 데이터


### 응답 프로토콜

- Status Line : HTTP버전 + 공백 + 상태코드 + 공백 + 상태 문구
    - 200 : 요청 성공 / 400 : 클라이언트측에 원인이 있는 에러 / 500 : 서버측에 원인이 있는 에러
- Headers : 옵션들
- Body : 데이터 응답시 보내는 데이터



### HTTP 헤더

- 일반 헤더
    - Content-Length : 메시지 바디 길이
    - Content-type : 메시지 바디에 들어있는 콘텐츠 종류 (ex. html 문서 → text/html)
- 요청 헤더
    - Cookie : 서버로부터 받은 쿠키를 다시 서버에 보내줌
    - Host : 요청된 URL에 나타낸 호스트명을 상세하게 표시 (HTTP 1.1에서 필수)
    - User-Agent : Client Program에 대한 식별 가능 정보를 제공 (모바일 버전, PC버전에 따라 값이 달라짐)
- 응답 헤더
    - Server : 사용하고 있는 웹 서버의 소프트웨어에 대한 정보를 포함
    - Set-Cookie : 쿠키를 생성하고 브라우저에 보낼 떄 사용. 해당 쿠키 값을 브라우저가 서버에게 다시 보낼 떄 사용

### URI (Uniform Resource Identifier)

인터넷 상에서 특정 자원을 나타내는 유일한 주소

- `scheme : //host[:port][/path][?query]`  구조
    - scheme : 요청 형식 지정 (보통 7계층) - http, ftp
    - host : 도메인 주소를 ip주소로 바꿔준다. (3계층)
    - port : 포트번호는 지정하지 않고 사용하면 http는 80번, https는 443번을 사용한다.
    - path : 파일의 경로
    - query : 프로그램 경로에 전달할 데이터
- **vs. URL (Uniform Resource Locator)**
    - uri : 자원의 위치 뿐만 아니라 자원에 대한 고유 식별자로서 url의 의미를 포함
    - url : 자원이 실제로 존재하는 위치
        - [`http://toto.co.kr/user/107`](http://torang.co.kr/user/107) 라고 했을 떄,
            - [`http://toto.co.kr/user`](http://toto.co.kr/user) 까지는 url이자 uri.
            - `/107` 까지 포함하면 식별자이므로 uri