### @Table

@Table은 엔티티와 매핑할 테이블을 지정하고 생략 시 매핑한 엔티티 이름을 테이블 이름으로 사용한다.

```
@Table(name="MEMBER")
public class Member {
  ...
}
```

### @Id

@Id는 JPA가 객체를 관리할 때 식별할 기본키를 지정한다.

### @GeneratedValue

@GeneratedValue는 기본 키 생성 전략으로 기본 키를 애플리케이션에 직접 할당하거나 자동 생성으로 키를 생성할 수 있다.

IDENTITY : 기본 키 생성을 데이터베이스에 위임
TABLE : 키 생성 테이블 사용

```
public class Member {
	@Id
	@GeneratedValue(strategy=GenerationType.IDENTITY)
	@Column(name = "ID")
	private Long id;
}
```

### @Column

@Column은 객체 필드를 테이블 컬럼에 매핑시켜주는 어노테이션이다.

	public class Member {
		@Id
		@GeneratedValue(strategy=GenerationType.IDENTITY)
		@Column(name = "ID")
		private Long id;
		
		@Column(length 15, nullable = false)
		private String name;
	}