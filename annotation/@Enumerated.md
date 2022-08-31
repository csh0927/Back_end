# @Enumrated

엔티티 매핑에서 Enum 타입을 사용할 때 @Enumrated 어노테이션을 사용한다.

**여기서 Enum이란**
enumerated type의 줄임말로 열거형이라고 부르기도 하는데 컴퓨터 프로그래밍에서 열거형(enumerated type, enumeration)은 요소, 멤버라 불리는 명명된 값의 집합을 이루는 자료형이다.

Enum 정의하는 방법

```
enum 열거형이름 {
    상수명1, 상수명2, 상수명n
}
```

이처럼 {}안에 상수의 이름을 나열하면 된다.

**@Enumerated**
@Enumerated 어노테이션의 종류는 두 가지이다.
``EnumType.ORDINAL`` : enum 순서(숫자) 값을 DB에 저장
`` EnumType.STRING`` : enum 이름 값을 DB에 저장

```
public enum OrderStatus {
  ORDER, CANCEL
}
```

다음과 같은 enum 클래스에서 어노테이션의 종류가 ``EnumType.ORDINAL`` 이라면 ORDER == 1로 저장, CANCEL == 2로 저장된다. 어노테이션의 종류가 `` EnumType.STRING`` 이라면 "ORDER", "CANCEL" 로 저장된다.