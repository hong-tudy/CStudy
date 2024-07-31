# HTTP & HTTPS

## HTTP

인터넷 상에서 클라이언트와 서버가 자원을 주고받을 떄 쓰는 통신 규약

아래처럼 텍스트로 보내진다.

```java
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
```

- 단점
    - 보안 이슈 : 네트워크에서 신호를 가로챌 경우 내용이 노출된다.
        - 대안 : HTTPS

## HTTPS

인터넷 상에서 정보를 암호화하는 SSL 프로토콜을 사용해 클라이언트와 서버가 자원을 주고받을 때 쓰는 통신 규약

- vs. HTTP
    - http는 텍스트 교환이지만, https는 텍스트를 암호화한다.
- 작동방식
    - 아래와 같이 응용계층에서 클라이언트가 HTTPS 요청을 생성한다. (http와 동일한 텍스트 형식)
        
        ```java
        GET /index.html HTTP/1.1
        Host: www.example.com
        
        ```
        
    - 표현계층에서 SSL/TLS 프로토콜을 통해 데이터를 암호화한다. 이 과정에서 클라이언트와 서버 간이ㅡ 핸드 셰이크가 이루어집니다.

### HTTP와 HTTPS의 차이

- HTTP의 동작 순서 : TCP → HTTP
- HTTPS의 동작 순서 : TCP → SSL → HTTP

SSL프로토콜을 쓰는지 여부의 차이다. 문서 전송 시 암호화 처리 여부에 따라 HTTP와 HTTPS로 나뉜다.

모든 사이트가 HTTPS로 하지 않는 이유? 암호화 과정으로 인한 속도 저하 발생