# DI, IoC

### DI

먼저 Dependency(의존 관계)란  A가 B를 의존한다라고 한다면, B가 변경되면 A에 영향을 미치며, A와 B는 의존 관계라고 할 수 있다.
DI란 외부에서 두 객체 간의 관계를 결정해주는 디자인 패턴으로, 인터페이스를 사이에 둬서 클래스 레벨에서는 의존관계가 고정되지 않도록 하고 런타임 시에 관계를 동적 주입하여 유연성 확보, 결합도를 낮출 수 있게 한다.

그럼 이 **DI(의존성 주입)**를 어떻게 **구현**할까?

**생성자 주입**생성자에 **@Autowired** 어노테이션을 붙여 의존성을 주입받는다. 호출시점에(해당클래스의 인스턴스생성시)1회 호출되는것이 보장된다.따라서 주입받은 객체가 변하지 않거나, 반드시 객체주입이 필요한 경우에 강제하기 위해 사용

```
@Service
public class BugService {

    private BugRepository bugRepository;

    public BugService(BugRepository bugRepository){
        this.bugRepository = bugRepository;
    }
}

```

**필드 주입**변수 선언부에 **@Autowired** 어노테이션을 붙인다.(편하지만 단일 책임 원칙 위반 가능성이 커지고 의존성이 숨는 등 단점이 많다.)

```
@Service
public class BugService {

    @Autowiroed
    private BugRepository bugRepository;
}

```

**수정자(setter) 주입**setter메소드에 **@Autowired** 어노테이션을 붙인다. 주입받는 개체가 변경될 가능성이 있는 경우에 사용한다.

```
@Service
public class BugService {

    private BugRepository bugRepository;

    @Autowired
    public void setBugRepository(BugRepository bugRepository) {
        this.bugRepository = bugRepository;
    }
}

```

**@Autowired** : 스프링 프레임워크에서 관리하는 Bean 객체와 같은 타입의 객체를 찾아서 자동으로 주입해주는 것. 해당 객체를 Bean으로 등록하지 않으면 주입해줄 수 없다.

### IoC

IoC(Inversion of Control)란 제어의 역전이라고 한다. 스프링 애플리케이션에서는 빈의 생성과 의존 관계 설정, 사용, 제거 등의 작업을 애플리케이션 코드대신 스프링 컨테이너가 담당한다. 이를 스프링 컨테이너가 코드 대신 빈에 대한 제어권을 갖고 있다고 해서 IoC라고 부른다. 따라서, 스프링 컨테이너를 IoC 컨테이너라고도 부른다.

**빈 팩토리**
스프링 컨테이너의 최상위 인터페이스, 스프링 빈을 관리하고 조회, 대표적으로 getBean() 메소드를 제공한다.

**애플리케이션 컨텍스트**
빈 팩토리 기능을 모두 상속받아서 제공한다.
