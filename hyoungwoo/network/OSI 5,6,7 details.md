### 5계층 - 세션 계층

- 세션
    - 두 통신 장치(호스트) 간의 대화가 이루어지는 논리적인 연결 상태를 의미
- 세션을 설정, 관리, 해제
    - 세션을 설정 및 해제하는 기능
- 대화 관리
    - 통상, 토큰을 사용함으로써 대화를 관리
        - 성립된 세션을 통한 상호 대화 관리를 하는 양단간 응용 개체를 위해 토큰 개념이 정의
        - 누가 언제 통신하였는지를 결정하며 토큰을 교환함으로써 구현
        - 프로세스는 토큰을 가졌을 때 전송할 수 있음
    - 여기서 토큰은 어떤 서비스의 실행을 기동하는 권리를 표현
- 다중화(multiplexing)
    - 효울을 높이기 위해, 여러 세션들을 묶어, 1개의 같은 전송계층 접속을 사용할 수 있음
        - 반대로 1개 세션이 속도 등을 위해 다수의 전송계층 접속들을 사용할 수도 있음
    - 따라서 전송 계층에서와 같이 세션 계층에서도 상향, 하향, 다중화가 가능
- 대화 단위별 그룹화
    - 세션계층은 전송 시 점검점, 동기점 등을 삽입함으로써 메세지를 대화 단위로 그룹화 함
    - 만일, 중간에 에러 발생하면 중단된 대화 단위부터 전송을 다시 시작
- 데이터의 범주화 교환
    - OSI는 데이터를 4가지 범주로 구분한 바 있음
    - 정보 데이터
        - 실제 전송되는 유용한 데이터
    - 급송 데이터
        - 긴급하게 전송되어야 하는 데이터
    - 제어 데이터
        - 세션 및 대화 관리를 위한 데이터
    - 세션 파라미터 협상에 사용되는 데이터
        - 세션 설정 시 파라미터를 협상하기 위한 데이터
- www.naver.com을 입력했을 때, 세션 계층이 하는 역할
    - 세션 설정
        - 애플리케이션 간의 통신 세션을 설정하고 유지하기 위한 논리적 구조를 제공
    - 데이터 전송
        - 데이터 흐름관리
            - 대화의 상태를 관리하고, 필요 시 오류 복구와 흐름 조절을 지원
        - 대화 관리
            - 요청과 응답 사이의 순서를 관리
                - 토큰은 세션을 식별하고, 두 시스템 간의 상호작용을 구분하며, 대화의 상태를 추적하는 데 사용
    - 세션 해제
        - 연결 종료
            - 모든 데이터 전송이 완료되면 세션 계층은 통신을 종료를 관리
                - 실제 연결 종료 절차는 전송 계층(TCP)에서 이루어지지만, 세션 계층은 세션 종료 절차를 논리적으로 처리하며, 양쪽 모두 데이터 전송이 끝났음을 확인하고, 세션을 안전하게 종료하도록 관리

### 6계층 - 표현 계층

- 네트워크 상의 여러 시스템들이 서로 다른 데이터 표현 방식을 사용하는데, 이를 하나의 통일된 구문 형식으로 변환시키는 기능을 수행
- 데이터 값이 다양한 여러 시스템에서 다른 방법으로 표현 및 저장
    - 예시
        - 정수형 값은 시스템에 따라 16비트, 24비트, 36비트 등으로 표현되는데
            - 두 응용 계층 프로토콜 개체가 서로 통신할 때, 양쪽 개체 간의 메세지가 같은 뜻으로 (공통의 어휘로) 교환되어야 함
    - 두 응용계층 간의 메세지 교환은 동일한 가상의 문법이 상호합의되어야 하는데 이런 번역기/변환기 역할을 수행하는 계층
- 기능
    - 응용 계층의 다양한 표현 양식을 공통의 형식으로 변환
        - 서로 다른 시스템이 사용하는 데이터 형식을 공통된 형식으로 변환
    - 암호화
        - 전송 중 데이터가 안전하도록 암호화
    - 압축
        - 데이터를 압축하여 전송 속도를 높이고 네트워크 사용을 줄임
            - 큰 이미지 파일을 압축하여 네트워크를 통해 빠르게 전송
    - 코드 변환
        - 데이터의 코드나 포맷을 서로 다른 시스템 간에 맞게 변환
            - 텍스트 파일의 인코딩 방식(UTF-8, ASCII 등)을 맞추어 변환
    - 가상 터미널 규약
        - 텍스트 터미널과 화면의 특성을 통일
            - 텍스트의 줄 길이, 페이지 모드, 커서의 위치 등을 표준화하여 서로 다른 시스템 간에 동일한 터미널 환경을 제공
- www.naver.com을 입력했을 때, 표현 계층이 하는 일
    - 웹 서버와 웹 브라우저 간의 데이터 형식을 통일
    - 암호화 및 복호화 작업을 통해 데이터의 보안을 유지
    - 데이터를 압축하여 전송 효율을 높임
    - 문자 인코딩과 같은 코드 변환을 통해 데이터의 일관성을 보장

### 7계층 - 응용 계층

- 응용
    - 다양한 범주의 정보처리 기능들을 총칭
- 응용 프로그램
    - 컴퓨터 사용자와의 상호작용을 통해, 특정 작업을 처리하는 특정 소프트웨어
        - 웹 브라우저, 이메일 클라이언트, 파일 전송 프로그램 등
- 응용 계층이란?
    - 여러 하위 통신 프로토콜 개체들에 대해, 사용자 관점의 인터페이스를 제공하는 통신 계층
    - 네트워크 상의 애플리케이션과 사용자 간의 상호작용을 가능하게 하며, 네트워크 서비스를 응용 프로그램에 제공하는 역할
- 기능
    - 통신 프로세스들 사이의 데이터 정의 및 처리
        - 응용 계층 프로세스들 사이의 통신은 하위 표현 계층이 제공하는 서비스를 이용
            - 데이터를 정의하고, 부호화하고, 암호화하고, 압축하는 서비스를 통하여 이루어짐
    - 서비스 제공
        - 네트워크 애플리케이션과 관련된 여러 서비스를 제공
        - 프로토콜을 통해 이루어짐
            - **SMTP (Simple Mail Transfer Protocol)**: 이메일 전송을 위한 프로토콜.
            - **HTTP (Hypertext Transfer Protocol)**: 웹 페이지를 전송하는 데 사용되는 프로토콜.
            - **HTTPS (Hypertext Transfer Protocol Secure)**: HTTP에 보안 기능을 추가하여 데이터 전송의 안전성을 보장하는 프로토콜.
    - www.naver.com을 입력했을 때, 표현 계층이 하는 일
        - 요청 생성
            - 웹 브라우저의 동작
                - 웹 브라우저(예: Chrome, Firefox, Edge)는 HTTP(S) 프로토콜을 사용하여 해당 웹사이트에 대한 요청을 생성
            - HTTP 요청
                - 웹 브라우저는 HTTP GET 요청을 생성하여 웹 서버에 전송
                    - 웹 페이지를 요청하는 정보를 포함
        - 프로토콜 처리
            - HTTP/HTTPS 프로토콜
                - 응용 계층에서 HTTP 또는 HTTPS 프로토콜을 사용하여 요청을 포맷하고 서버에 전달
            - 보안
                - HTTPS의 경우, 응용 계층에서 SSL/TLS를 사용하여 데이터를 암호화하여 보안성을 높임
        - 응답 처리
            - 서버 응답 수신
                - 요청을 수신하고 처리하여 웹 페이지를 포함한 HTTP 응답을 브라우저로 보냄
            - 응답 해석
                - 브라우저는 수신한 HTTP 응답을 해석하고, 응답 헤더와 본문을 분리하여 웹 페이지를 렌더링
        - 데이터 표현
            - HTML/CSS/JavaScript
                - 브라우저는 HTML, CSS, JavaScript 등 다양한 웹 콘텐츠를 해석하여 사용자에게 표시
        - 세션 및 상태 관리
            - 쿠키와 세션
                - 웹 브라우저와 서버 간의 세션 관리와 상태 유지를 위해 쿠키와 세션 정보를 관리
                - 사용자가 웹사이트에 로그인하거나 특정 설정을 유지하는 데 필요