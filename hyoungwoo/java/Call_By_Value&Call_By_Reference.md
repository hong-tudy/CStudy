- **Call By Value (값에 의한 호출)**
    - 함수 호출 시, 실제 인자의 값이 함수의 매개변수에 복사되어 전달
    - 함수 내부에서 매개변수의 값을 변경하더라도 호출한 쪽의 변수에는 영향을 미치지 않음
        - 값만을 전달하기 때문에 수신자의 파라미터를 수정해도 호출자의 변수에는 아무런 영향이 없음
    - 메서드를 호출하는 호출자 (Caller) 의 변수와 호출 당하는 수신자 (Callee) 의 파라미터는 복사된 **서로 다른 변수**
- **Call By Reference (참조에 의한 호출)**
    - 함수 호출 시, 실제 인자의 주소(참조)가 전달
    - 함수 내부에서 매개변수를 수정하면 호출한 쪽의 변수에도 영향
        - 메서드 내에서 파라미터를 수정하면 그대로 원본 변수에도 반영
    - 참조를 직접 넘기기 때문에 호출자의 변수와 수신자의 파라미터는 **완전히 동일한 변수**
- Java에서의 파라미터 전달 방법
    - **오직 Call by Value 로만 동작**
    - JVM 메모리에 변수가 저장되는 위치
        - 변수를 선언하면 Stack 영역에 할당
        - 원시 타입 (Primitive Type) 은 Stack 영역에 변수와 함께 저장
        - 참조 타입 (Reference Type) 객체는 Heap 영역에 저장되고 Stack 영역에 있는 변수가 객체의 주소값
    - 원시 타입 (Primitive Type)의 전달
        - 원시 타입은 Stack 영역에 위치
        - 예시 코드
        
        ```java
        public class PrimitiveTypeTest {
        
            @Test
            @DisplayName("Primitive Type 은 Stack 메모리에 저장되어서 변경해도 원본 변수에 영향이 없다")
            void test() {
                int a = 1;
                int b = 2;
        
                // Before
                assertEquals(a, 1);
                assertEquals(b, 2);
        
                modify(a, b);
        
                // After: modify(a, b) 호출 후에도 값이 변하지 않음
                assertEquals(a, 1);
                assertEquals(b, 2);
            }
        
            private void modify(int a, int b) {
                // 여기 있는 파라미터 a, b 는 이름만 같을 뿐 test() 에 있는 a, b 와 다른 변수
                a = 5;
                b = 10;
            }
        }
        ```
        
        - 위 코드에서 `test()` 의 변수 `a`, `b` 와 `modify(a, b)` 로 전달받은 파라미터 `a`, `b` 의 이름과 값은 같지만 다른 변수
        - `modify(a, b)` 를 호출하는 순간 Stack 영역에 새로운 변수 `a`, `b` 가 새로 생성되어 총 4 개의 변수가 존재
        
        ![](https://raw.githubusercontent.com/ParkJiwoon/PrivateStudy/master/java/images/screen_2022_01_30_22_01_33.png)
        
        - `modify()` 영역의 값을 바꿔도 `test()` 영역의 변수는 변화가 없음
        - **원시 타입의 전달은 값만 전달하는 Call by Value 로 동작**
    - 참조 타입 (Reference Type)의 전달
        - 변수 자체는 Stack 영역에 생성되지만 실제 객체는 Heap 영역에 위치
            - Stack 에 있는 변수가 Heap 에 있는 객체를 바라보고 있는 형태
        - 예시코드
        
        ```java
        class User {
            public int age;
        
            public User(int age) {
                this.age = age;
            }
        }
        
        public class ReferenceTypeTest {
        
            @Test
            @DisplayName("Reference Type 은 주소값을 넘겨 받아서 같은 객체를 바라본다" +
                         "그래서 변경하면 원본 변수에도 영향이 있다")
            void test() {
                User a = new User(10);
                User b = new User(20);
        
                // Before
                assertEquals(a.age, 10);
                assertEquals(b.age, 20);
        
                modify(a, b);
        
                // After
                assertEquals(a.age, 11);
                assertEquals(b.age, 20);
            }
        
            private void modify(User a, User b) {
                // a, b 와 이름이 같고 같은 객체를 바라본다.
                // 하지만 test 에 있는 변수와 확실히 다른 변수다.
        
                // modify 의 a 와 test 의 a 는 같은 객체를 바라봐서 영향이 있음
                a.age++;
        
                // b 에 새로운 객체를 할당하면 가리키는 객체가 달라지고 원본에는 영향 없음
                b = new User(30);
                b.age++;
            }
        }
        ```
        
        - 원시 타입 코드와 마찬가지로 동일한 변수 `a`, `b` 가 존재
        - `modify(a, b)` 를 호출한 후에 `a.age` 의 값이 변경되었기 때문에 Call by Reference 로 파라미터를 넘겨주었다고 착각하기 쉽지만, **Reference 자체를 전달하는 게 아니라 주소값만 전달**해주고 `modify()` 에서 생긴 변수들이 주소값을 보고 객체를 같이 참조하고 있는 것
        - 처음 선언 시 메모리 상태
            - 원시 타입과는 다르게 변수만 Stack 영역에 생성되고 실제 객체는 Heap 영역에 생성
            - 각 변수는 Heap 영역에 있는 객체를 바라보고 있음
        
        ![](https://raw.githubusercontent.com/ParkJiwoon/PrivateStudy/master/java/images/screen_2022_01_30_22_44_00.png)
        
        - **`modify(a, b);`** 호출 시점의 메모리 상태
            - 넘겨받은 파라미터는 Stack 영역에 생성되고 넘겨받은 주소값을 똑같이 바라봄
        
        ![](https://raw.githubusercontent.com/ParkJiwoon/PrivateStudy/master/java/images/screen_2022_01_30_22_50_06.png)
        
        - **`modify(a, b);`** 수행 직후 메모리 상태
            - `test()` 영역과 `modify()` 영역에 존재하는 `a` 라는 변수들은 같은 객체인 `User01` 을 바라보고 있기 때문에 객체를 공유
            - `b` 라는 변수는 서로 같은 객체인 `User02` 를 바라보고 있었지만 `modify(a, b)` 내부에서 새로운 객체를 생성해서 할당했기 때문에 `User03` 이라는 객체를 바라봄
                - `User03` 의 `age` 값을 변경해도 `test()` 에 있는 `b` 에는 아무런 변화가 없음
        
        ![](https://raw.githubusercontent.com/ParkJiwoon/PrivateStudy/master/java/images/screen_2022_01_30_23_12_16.png)
        
        - test() 메서드가 끝난 후 최종 메모리 상태
            - `modify(a, b)` 메서드를 빠져나오면 Stack 영역에 할당된 변수들은 사라짐
            - 최종적으로 위와 같은 상태가 되며 `User03` 은 어떤 곳에서도 참조되고 있지 않기 때문에 나중에 Garbage Collector 에 의해 제거
        
        ![](https://raw.githubusercontent.com/ParkJiwoon/PrivateStudy/master/java/images/screen_2022_01_30_23_15_36.png)
        
- 결론
    - Java는 Call By Reference 같은 Call By Value를 사용
        - Call by Reference 는 참조 자체를 넘기기 때문에 새로운 객체를 할당하면 원본 변수도 영향
        - 객체를 넘기고 객체 내용의 값을 변경하면 호출한 쪽에서도 값이 변경되지만, 참조를 다른 객체로 변경하면 호출한 쪽의 참조에는 영향을 미치지 않음
    - **가장 중요한 논점은 호출자 변수와 수신자 파라미터는 Stack 영역 내에서 각각 존재하는 다른 변수**