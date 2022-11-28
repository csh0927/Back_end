## 연관관계 매핑

**연관관계 매핑이란**, 객체의 참조와 테이블의 외래 키를 매핑하는 것을 의미한다.

* JPA에서는 연관 관계에 있는 상대 테이블의 PK를 멤버 변수로 갖지 않고, 엔ㅌ티ㅣ 객체 자체를 통째로 참조한다.

#### 1. 방향

* 단방향 관계 : 두 엔티티가 관계를 맺을 때, 한 쪽의 엔티티만 참조하고 있는 것을 의미
* 양방향 관계 : 두 엔티티가 관계를 맺을 때, 양 쪽이 서로 참조하고 있는 것을 의미

#### 2. 다중성

관계에 있는 두 엔티티는 다음 중 하나의 관계를 갖는다.

* ManyToOne : 다대일 (N : 1)
* OneToMany : 일대다 (1 : N)
* OneToOne : 일대일 (1 : 1)
* ManyToMany : 다대다 (N : N)

예를 들면, 하나의 Team은 여러 Member를 구성원으로 갖고 있으므로 Team 입장에서는 Member와 일대다 관계이며, Member의 입장에서는 하나의 Team에 속하므로 다대일 관계이다.

즉, 어떤 엔티티를 중심으로 상대 엔티티를 바라보느냐에 따라 다중성이 달라지게 된다.

#### 3. 연관관계 주인(Owner)

객체를 양방향 연관관계로 만들면 연관관계의 주인을 정해야 한다.

* 연관관계를 갖는 두 테이블에서 외래키를 갖게되는 테이블이 연관관계의 주인이 된다.
* 연관관계의 주인만이 외래 킼를 관리(등록, 수정, 삭제)할 수 있고, 주인이 아닌 엔티티는 읽기만 할 수 있다.

#### 1) @ManyToOne - 단방향

```
@Entity
@Getter @Setter
public class Member {
 
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
 
    @Column(nullable = false)
    private String username;
 
    @ManyToOne
    @JoinColumn(name = "TEAM_ID")
    private Team team;
}

-----------------------------------------------------------------
 
@Entity
@Getter @Setter
public class Team {
 
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
 
    @Column(nullable = false)
    private String name;
}
```

단방향은 한 쪽의 엔티티가 상대 엔티티를 참조하고 있는 상태이기 때문에 Member 엔티티에만 @ManyToOne 어노테이션이 있다.

* Membe 입장에선 Team과 다대일 관계이므로 @ManyToOne이 된다.
* @JoinColumn(name = "TEAM_ID")
  * @JoinColumn 어노테이션은 외래 키를 매핑할 때 사용한다. name 속성에는 매핑 할 외래 키 이름을 지정한다.
  * Member 엔티티의 경우 Team 엔티티의 id 필드를 외래 키로 가지므로, TEAM_ID

####2) OneToMany - 양방향

```
@Entity
@Getter @Setter
public class Team {
 
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
 
    @Column(nullable = false)
    private String name;
 
    @OneToMany(mappedBy = "team")
    private List<Member> members = new ArrayList<>(); 
}
```

Team은 Member를 Lisst로 가지며, 연관관계의 주인을 정하기 위해 @OneToMany에 mappedBy 속성 추가

연관관계의 주인을 정하는 방법은 mappedBy 속성을 지정하는 것

* 주인은 mappedBy 속성을 사용하지 않고, @JoinColumn을 사용
* 주인이 아닌 엔티티 클래스는 mappedBy 속성을 사용해 주인을 정할 수 있다.
  * 주인은 mappedBy 속성을 사용할 수 없으므로 연관관계의 주인이 아닌 Team 엔티티에서 members 필드에 mappedBy의 속성으로 Member 테이블의 Team 필드 이름을 명시해준다.

#### 3) OneToOne - 단방향

한 유저가 한 개의 블로그만 만들 수 있는 서비스가 있다고 가정한다면, 유저와 블로그는 1:1 관게일 것이다.

유저 엔티티 입장에서 블로그의 @Id를 외래 키로 가져서 블로그를 참조할 수 있고,그 반대 경우인 블로그가 외래키를 가져서 유저를 참조하는 것도 가능하다. 여기서 **외래 키를 갖고 있는 테이블을 주 테이블**이라고 한다.

(밑에 있는 코드는 유저에 외래키를 두는 방식)

```
@Entity
@Getter @Setter
public class User {
    
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long no;
    
    @Column(nullable = false)
    private String id;
    
    @OneToOne
    @JoinColumn(name = "blog_no")
    private Blog blog;
}

------------------------------------------------------------------
 
@Entity
@Getter @Setter
public class Blog {
 
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long no;
 
    @Column(nullable = false)
    private String address;
}
```

#### 4) OneToOne - 양방향

```
@Entity
@Getter @Setter
public class Blog {
 
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long no;
 
    @Column(nullable = false)
    private String address;
    
    @OneToOne(mappedBy = "blog")
    private User user;
}
```

양방향 관계이기 때문에 연관관계의 주인을 정해야 한다. (User 클래스는 동일)