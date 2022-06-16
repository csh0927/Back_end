### @Entity

@Entity 어노테이션은 데이터베이스의 테이블과 일대일로 매칭되는 객체 단위이며 Entitiy 객체의 인스턴스 하나가 테이블에서 하나의 레코드 값을 의미한다.

```
@Entity
@Table(name = "EMPLOYEE")
public class Employee {
  ...
}
```

### @Repository

@Repository 어노테이션은 DAO를 인식시켜주기 위한 설정이다. 해당 클래스가 DAO라는 것을 알리기 위해서 @Repository라고 적어준다. DAO는 데이터베이스에 접근하기 위한 객체이다.

```
 @Repository("userDAO")
public class UserDAO {
  ...
}
```

