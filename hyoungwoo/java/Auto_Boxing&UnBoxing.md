- 자바에는 기본형 타입과 `Wrapper` 클래스가 존재
    - 기본 타입
        - 정수형 : byte, short, int, long
        - 실수형 : float, double
        - 문자형 : char
        - 진위형 : boolean
    - `Wrapper` 클래스
        - 정수형 : Byte, Short, Integer, Long
        - 실수형 : Float, Double
        - 문자형 : Character
        - 진위형 : Boolean
- 박싱 (Boxing)
    - 기본 타입 데이터에 대응하는 Wrapper 클래스로 만드는 동작
- 언박싱 (UnBoxing)
    - Wrapper 클래스에서 기본 타입으로 변환

```java
// 박싱
int i = 10;
Integer num = new Integer(i);

// 언박싱
Integer num = new Integer(10);
int i = num.intValue();
```

### **오토 박싱 & 오토 언박싱**

- JDK 1.5부터는 자바 컴파일러가 박싱과 언박싱이 필요한 상황에 자동으로 처리
- 오토 박싱
    - 기본형 타입 데이터를 해당하는 래퍼 클래스의 객체로 자동 변환하는 것
- 오토 언박싱
    - 래퍼 클래스를 해당 기본형 타입으로 자동 변환하는 것

```java
// 오토 박싱
int i = 10;
Integer num = i;

// 오토 언박싱
Integer num = new Integer(10);
int i = num;
```

- 성능
    - stream을 사용할때도 내부적으로 오토 박싱이 일어나고 이로 인해서 잘못 사용하는 경우 일반적은 반복문 보다 성능이 나오지 않는 경우가 발생
        - Wrapper 클래스의 값을 비교할 때는 equals() 메서드를 사용해야 하는데 이는 값의 비교가 아닌 객체의 비교를 수행하므로성능 저하가 발생할 수 있음
        - 기본 타입의 값을 비교할 때는 == 연산자를 사용하는 것이 좋음
    - 편의를 위해 자동으로 처리하지만 내부적인 추가 연산 작업이 거치게 됨
        - 오토박싱을 사용할 경우 기본 타입의 값을 Wrapper 클래스 객체로 변환하는 과정에서 새로운 객체가 생성
        - 메모리 할당 가비지 컬렉션 등의 부하가 발생하므로 성능 저하가 발생할 수 있음
            - new 연산자가 비용이 큼
    - 따라서, 오토 박싱&언박싱이 일어나지 않도록 동일한 타입 연산이 이루어지도록 구현하는 것이 좋음