![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/da50Yz/btq0Dsje4ZV/lGe8H8nZgdBdgFvo7IczS0/img.png)

### **Blocking/Non-blocking**

- 호출된 함수가 호출한 함수에게 제어권을 건내주는 유무의 차이
- 제어권
    - 함수의 코드나 프로세스의 실행 흐름을 제어할 수 있는 권리
- **Blocking**
    - 자신의 작업을 진행하다가 다른 주체의 작업이 시작되면 다른 작업이 끝날 때까지 기다렸다가 자신의 작업을 시작하는 것을 의미
    - 호출된 함수가 자신이 할 일을 모두 마칠 때까지 제어권을 계속 가지고서 호출한 함수에게 바로 돌려주지 않는 상황을 의미
- **Non-blocking**
    - 다른 주체의 작업에 관련없이 자신의 작업을 하는 것을 의미
    - 호출된 함수가 자신이 할 일을 모두 마치지 않았더라도 바로 제어권을 건네주어 호출한 함수가 다른 일을 진행할 수 있도록 해주는 상황을 의미

### **Synchronous/Asynchronous**

- 결과를 돌려주었을 때 순서와 결과에 관심이 있는지 없는지로 판단
- 동기/비동기는 요청한 작업에 대해 완료 여부를 신경 써서 작업을 순차적으로 수행할지 아닌지에 대한 관점
- **Synchronous**
    - 동기라는 뜻으로 작업을 동시에 수행하거나, 동시에 끝나거나, 끝나는 동시에 시작함을 의미
    - 호출된 함수의 수행 결과 및 종료를 호출한 함수와 함께 신경 쓰는 경우를 의미
- **Asynchronous**
    - 비동기라는 뜻으로 시작과 종료가 일치하지 않고 끝나는 동시에 시작을 하지 않음을 의미
    - 호출된 함수의 수행 결과 및 종료를 호출된 함수 혼자 직접 쓰고 처리하는 경우를 의미
- Blocking / Non-Blocking
    - 호출된 함수가 호출한 함수에게 제어권을 바로 주느냐 안주느냐
- Sync / Async
    - 호출된 함수의 종료를 호출한 함수가 처리하느냐, 호출된 함수가 처리하느냐의 차이

### 비동기의 성능적 이점

- 요청한 작업에 대하여 완료 여부를 신경쓰지 않고 자신의 그다음 작업을 수행한다는 것은, I/O 작업과 같은 느린 작업이 발생할 때, 기다리지 않고 다른 작업을 처리하면서 동시에 처리하여 멀티 작업을 진행할수 있기 때문
- 동시처리
    - 멀티 스레드, 멀티 프로세싱

## 동기/비동기 + 블로킹/논블로킹 조합

### **Blocking & Synchronous**

- 다른 작업이 진행되는 동안 자신의 작업을 처리하지 않고 (Blocking), 다른 작업의 완료 여부를 바로 받아 순차적으로 처리하는 (Sync) 방식
- 다른 작업의 결과가 자신의 작업에 영향을 주는 경우에 활용
- 예시
- Node.js에서 코드 실행 시점을 늦춰주거나 순차적인 의존성이 있는 작업을 처리할 때는 동기 & 블로킹 방식을 사용하여 작업의 순서와 타이밍을 제어할 수 있도록 함
- 파일을 읽어 내용을 처리하는 로직
    - 파일을 먼저 읽어야 그다음 작업을 처리할 수 있음
        - 작업량이 많거나 시간이 오래 걸리는 작업을 처리해야 하는 경우에는 Sync Blocking 방식을 사용하면 독이 됨
    - C나 Java의 코드 실행 후 커맨드에서 입력을 받는 경우
        - 입력을 받아 입력값을 가지고 내부 처리를 하여 결과값을 콘솔에 출력하기 때문에 순차적인 작업

### **Blocking & Asynchronous**

- 다른 작업이 진행되는 동안 자신의 작업을 멈추고 기다리는 (Blocking), 다른 작업의 결과를 바로 처리하지 않아 순서대로 작업을 수행하지 않는 (Async) 방식
- Async-blocking 의 경우는 실무에서 잘 마주하기 쉽지 않아 다룰일이 거의 없음
- 예시
    - Node.js + MySQL의 조합
        - Node.js에서 비동기 방식으로 데이터베이스에 접근하기 때문에 Async 이지만, MySQL 데이터베이스에 접근하기 위한 MySQL 드라이버가 블로킹 방식으로 작동
        - 과정
            
            ```
            JavaScript는 비동기 방식으로 MySQL에 쿼리를 보낸다. (Async)
            MySQL은 쿼리를 처리하면서 JavaScript에게 제어권을 넘겨주지 않는다. (Blocking)
            그러면 JavaScript는 다른 작업을 계속 수행할 수 있지만, MySQL의 결과값을 필요로 하기 때문에 MySQL이 쿼리를 완료할 때까지 기다려야 된다.
            결국 Sync Blocking과 작업 수행에 차이가 없게 된다
            ```
            
        

### **Non-blocking & Synchronous**

- Non-blocking : A 함수가 B 함수를 호출 한 뒤, B 함수가 A 함수에게 제어권을 바로 돌려준다.
- Synchronous : A 함수가 B 함수를 호출 할 때, B 함수의 결과를 A 함수가 처리하는 것.
- B 함수가 바로 제어권을 돌려주기에 A 함수는 다른 작업을 수행할 수 있지만, 언제 종료되는지 알 수 없는 B 함수의 종료를 A 함수가 처리해야 함
- A 함수가 직접 결과를 처리해야하는 상황이기에 B 함수의 종료를 반복적으로 물어봐야 하는 경우
- 예시
    - 자바
        - 스레드(Thread) 객체를 만들어 요청 작업을 백그라운드에 돌게 하고 메인 메서드에서 while문을 통해 스레드가 모두 처리되었는지 끊임없이 확인하고, 처리가 완료되면 다음 메인 작업을 수행
        - Tip
            
            ```
            async/await은 비동기 논블로킹 방식을 동기 논블로킹 방식으로 바꿔주는 기법이라고 할 수 있지만, 그러나 async/await은 내부적으로는 여전히 비동기 논블로킹 방식으로 동작한다는 점은 유의하자. async 함수 자체가 메인 콜 스택(call stack)이 모두 실행되어 비워져야 수행하기 때문에 비동기 논블로킹이기 때문이다.
            ```
            
    - 게임에서 맵을 이동할때
        - 맵 데이터를 모두 다운로드
        - 화면에는 로딩 스크린
        - 로딩 스크린은 로딩바가 채워지는 프로그램이 수행
        - 제어권은 여전히 나한테 있어 화면에 로드율이 표시되는 것
        - 끊임없이 맵 데이터가 어느정도 로드가 됬는지 끊임없이 조회
        - 자신의 작업을 계속하고 있지만 다른 작업과의 동기를 위해 계속해서 다른 작업이 끝났는지 조회하는 것

### **Non-blocking & Asynchronous**

- 다른 작업이 진행되는 동안에도 자신의 작업을 처리하고 (Non Blocking), 다른 작업의 결과를 바로 처리하지 않아 작업 순서가 지켜지지 않는 (Async) 방식
- 다른 작업의 결과가 자신의 작업에 영향을 주지 않은 경우에 활용
- 예시
    - Node.js에서 비동기 방식으로 파일을 읽거나 네트워크 요청을 보낼 때는 비동기 & 논블로킹 방식을 사용하여 작업이 완료될 때까지 다른 작업을 수행할 수 있도록 함
    - 파일 읽기
        - 작업량이 많거나 시간이 오래 걸리는 작업을 처리
    - 웹 브라우저의 파일 다운로드
        - 웹 사이트에서 파일을 다운로드할 때, 파일의 전송이 완료될 때까지 다른 작업을 하지 않고 기다리는 것이 아니라, 다른 탭이나 창을 열거나 웹 서핑을 할 수 있음
            - 웹 브라우저가 파일 다운로드를 비동기적으로 처리하고, 콜백 함수를 통해 다운로드가 완료되면 알려주는 방식으로 구현
Blocking I/O & Non-Blocking I/O
I/O 작업은 Kernel level에서만 수행할 수 있다. 따라서, Process, Thread는 커널에게 I/O를 요청해야 한다.


#Blocking I/O
I/O Blocking 형태의 작업은

(1) Process(Thread)가 Kernel에게 I/O를 요청하는 함수를 호출

(2) Kernel이 작업을 완료하면 작업 결과를 반환 받음.

특징
I/O 작업이 진행되는 동안 user Process(Thread) 는 자신의 작업을 중단한 채 대기
Resource 낭비가 심함
(I/O 작업이 CPU 자원을 거의 쓰지 않으므로)

여러 Client 가 접속하는 서버를 Blocking 방식으로 구현하는 경우 -> I/O 작업을 진행하는 작업을 중지 -> 다른 Client가 진행중인 작업을 중지하면 안되므로, client 별로 별도의 Thread를 생성해야 함 -> 접속자 수가 매우 많아짐

이로 인해, 많아진 Threads 로 컨텍스트 스위칭 횟수가 증가함,,, 비효율적인 동작 방식


#Non-Blocking I/O
I/O 작업이 진행되는 동안 User Process의 작업을 중단하지 않음.

진행 순서

User Process가 recvfrom 함수 호출 (커널에게 해당 Socket으로부터 data를 받고 싶다고 요청함)

Kernel은 이 요청에 대해서, 곧바로 recvBuffer를 채워서 보내지 못하므로, "EWOULDBLOCK"을 return함.

Blocking 방식과 달리, User Process는 다른 작업을 진행할 수 있음.

recvBuffer에 user가 받을 수 있는 데이터가 있는 경우, Buffer로부터 데이터를 복사하여 받아옴.

이때, recvBuffer는 Kernel이 가지고 있는 메모리에 적재되어 있으므로, Memory간 복사로 인해, I/O보다 훨씬 빠른 속도로 data를 받아올 수 있음.

recvfrom 함수는 빠른 속도로 data를 복사한 후, 복사한 data의 길이와 함께 반환함.