# TCP 프로토콜과 UDP 프로토콜

## UDP 프로토콜의 구조
[!udp프로토콜](./images/udp_protocol.png)
- **Source Port(2byte)** : 출발지 포트 번호
    - 포트번호는 0번 부터 65535번(FFFF)까지 있음 (∵ 16진수 한 자리가 4bit)
- **Destination Port(2byte)** : 목적지 포트 번호
- **Length(2byte)** : UDP 프로토콜 헤더와 페이로드를 포함한 길이
- **Checksum(2byte)** : 프로토콜의 오류를 체크하는 값

## UDP 프로토콜의 특징

- 사용자 데이터그램 프로토콜
    - 데이터그램 : 독립적인 패킷 (비연결 프로토콜인 UDP는 TCP와는 달리 각각의 패킷이 독립적으로 전송된다)
- 비연결지향형
- UDP 전송 방식은 너무 단순해서 서비스의 신뢰성이 낮고, 데이터 그램 도착 순서가 바뀌거나 중복되거나 심지어는 통보없이 누락시키기도 함.
    - 일반적으로 오류의 검사와 수정이 필요없는 프로그램에서 수행할 것으로 가정




## TCP 프로토콜의 구조
[!tcp프로토콜](./images/tcp_protocol.png)
- **Source Port**
- **Destination Port**
- **Sequence Number**
- **Acknowledgement Number**
- **TCP Options** → 최대 60바이트, but 옵션 잘 안 붙음
- **Offset** → 헤더의 길이 (4로 나눔)
- **Reserved** → 예약된 필드, 사용 안 함
- **Window** → 데이터 얼마만큼 더 보내도 된다는 걸 상대방에게 알려주는 곳
- **Urgent Pointer →**
- TCP Flags : 데이터를 보낼 때, 어떤 형태로 보내지는지를 나타냄
    - Urgent → 긴급 비트 ( 우선순위가 높은 데이터)
        - Urgent Pointer → 어디서부터 긴급데이터인지 나타내는 위치값
    - Acknowledgement → 승인 플래그 ( 데이터를 보내도 되는지 안되는지 승인하는 데이터 )
    - Push → 밀어넣기 비트( TCP 버퍼가 일정 크기만큼 쌓여야 추가적으로 전송하는데 이와 상관없이 데이터를 밀어넣겠다. 많이 사용 x )
    - Reset → 초기화 비트 ( 상대방과 연결된 상태에서 데이터를 주고받으려는데 문제가 발생했을 시 연결을 reset)
    - `S`yn → 동기화 비트 ( 상대방과 연결을 시작할 때 무조건 사용. 얘가 처음 보내지고 나서 둘 사이의 연결이 서로 동기화되기 시작)
    - Fin → 종료 비트 ( 데이터를 다 주고받은 뒤에 연결을 끊을 때TCP)
## TCP 프로토콜의 특징

- 인터넷에 연결된 컴퓨터에서 실행되는 프로그램 간에 통신을 안정적으로, 순서대로, 에러없이 교환할 수 있게 한다.
- TCP의 안정성을 필요로 하지 않을 때 일반적으로 TCP 대신 UDP를 사용한다.
- TCP는 UDP보다 안전하지만 느리다.


## 포트

- TCP나 UDP에서 애플리케이션이 상호 통신을 위해 사용하는 가상의 논리적 통신 연결단 / 해당 IP 주소가 가리키는 PC에 접속할 수 있는 통로
- 특징
    - 프로세스간 통신을 위해 사용 → 컴퓨터가 아닌 프로그램이 사용
    - 하나의 포트는 하나의 프로세스만 사용 가능
    - 하나의 프로세스는 여러개의 포트 사용 가능
- 종류
    - Well-Known 포트
        - 전세계적으로 유명한 포트. 인터넷 주소 관리 기간 ICANN 이 애플리케이션 용으로 지정
        - (ex) HTTP : 80 / HTTPS : 443
    - Registered 포트
        - 유명회사들이 등록한 번호
        - (ex) mysql : 3306 / 오라클 : 1521
    - Dynamic 포트  ???
        - 일반 사용자들이 사용하는 번호. 주로 클라이언트 입장에서 사용하는 번호
        - (ex) chrome(49153) - 네이버 (4)