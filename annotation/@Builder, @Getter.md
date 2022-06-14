### @Builder

@Builder는 해당 클래스에 자동으로 빌더를 추가해준다. 빌더란 디자인 패턴 중 하나인 빌더 패턴을 의미한다. 객체 생성 방법과 표현 방법을 분리하는 것을 의미한다.

```
public class User {
  private final String name;
  private final int age;
  private final String email;
}

@Builder
public User(String name, int age, String email) {
  this.name = name;
  this.age = age;
  this.email = email;
}
```

### @Getter

@Getter는 인스턴스 변수를 반환한다. getter는 변수 앞에 get이 붙고 그 변수들의 앞글자는 대문자로 한다.

```
@Getter
public class Test {
  private String color;
  
  // Getter
  public String getColor() {
    return color;
  }
}
```