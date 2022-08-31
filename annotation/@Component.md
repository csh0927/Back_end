# @Component

@Component는 개발자가 직접 작성한 Class를 Bean으로 등록하기 위한 Annotation 이다. 

스프링의 컴포넌트 스캔 기능에 의해 스캔될 때, 주어진 패키지 내에서 @Component 어노테이션이 적용된 클래스를 식별하고, 그러한 클래스의 빈을 생성하여 ApplicationContext에 등록한다.

(value = "") 옵션이 있고, 해당 옵션을 사용하지 않는다면 class의 이름을 camelCase(카멜표기법)로 변경한 것을 bean id로 사용한다.