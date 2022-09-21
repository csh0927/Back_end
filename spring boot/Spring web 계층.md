## 1. WebLayer

* controllers, exception handlers, filters, view templates, etc.

개요 : 웹 어플리케이션의 최상위에 존재하며 외부 요청과 응답에 대한 전반적인 영역이며 어플리케이션의 진입점이기 때문에 다른 레이어에서 발생한 예외도 처리 한다. 인증을 관리하고 권한없는 사용자의 인가를 거부하는 역할도 한다.

포함 : 흔히 사용하는 컨트롤러(@Controller)와 JSP/Freemarker 등의 뷰 템플릿 영역이며, 필터(@Filter), 인터셉터, 컨트롤러 어드바이스(@ControllerAdvice) 등이 모두 Web Layer에 포함된다.

데이터 처리 : 데이터 전송 객체만 처리해야 한다.

## 2. Service Layer

* application sevice and infrastructure service

개요 : Web Layer 바로 아래 존재하는 객체로, 트랜잭션(Transaction, 데이터베이스의 상태를 변환시키는 하나의 논리적 기능을 수행하기 위한 작업의 단위)에 대한 경계 역할을 한다. 어플리케이션과 이프라 서비스를 모두 포함하고 있다.

포함 : @Service에 사용되는 서비스 영역. 일반적으로 Controller와 Dao 중간 영역에서 사용된다. @Transactional이 사용되어야 하는 영역이기도 하다.

데이터 처리 : 데이터 전송 객체를 메소드의 매개변수로 사용, 도메인 모델 객체를 처리. 그리고 데이터 전송 객체만 웹 레이어로 반환할 수 있다.

* 작성 시 주의사항 : Service는 다른 service를 조합하거나 DAO를 연결하는 역할을 수행, Service는 가볍게, Service에 비즈니스 로직을 구현하면 안된다.(비즈니스 로직은 도메인 모델에서 처리-후술)

## 3. Repository Layer

* repository interface and their implement

개요 : 가장 낮은 계층으로 사용되는 데이터 스토리지 계층과 통신하는 역할을 한다. 데이터베이스와 같이 데이터 저장소(repository)에 접근하는 역할이다.

포함 : Database와 같이 데이터 저장소에 접근하는 영역. Dao(Data Access Object)영역과 같은 의미이다.

데이터 처리 : 엔티티를 메소드 매개변수로 가져올 수 있고 엔티티를 리턴한다.

## 4. DTOs

개요 : DTO는 단순히 데이터를 저장하는 컨테이너, 즉 Data Transfer Object로, 다른 계층 간 교환을 위한 객체이다. DTOs는 이들이 존재하는 영역을 의미한다.

포함 : 뷰 템플릿 엔진에서 사용될 객체, Repository Layer에서 결과로 넘겨 준 객체 등이 DTO에 해당한다.

## 5. Domain Model

* Domain services, entities, and VO

개요 : Domain 은 Entity이고 전체 라이프 사이클 동안 변경되지 않는 객체이며 Value Obfect(VO: DTO와 동일 개념이나 readonly속성을 가짐)로, 속성이나 사물을 설명. Domain Model은 Domain을 모든 사람이 동일한 관점에서 이해, 공유할 수 있도록 단순화 시킨 것. VO등도 해당되므로 무조건 데이터베이스의 테이블과 관계가 있어야 하는 것은 아니다.

예시 : 택시 앱을 가정했을 때, 배차, 탑승, 요금 등이 모두 도메인이다.

## 6. 데이터 전송 객체를 사용하는 이유

* 클라이언트의 데이터를 이용하기 쉽도록 하기 위해
  * 도메인 모델은 애플리케이션의 내부 모델인다, 외부에 노출시킨다면 클라이언트는 내부 모델을 알지 못하는 상태에서 사용해야 한다. DTO를 통해 클라이언트에게 모델을 숨기고 더 사용하기 쉬운 API를 제공하는 것이 좋다.
* 유지 보수를 유연하게 하기 위해
  * 도메인 모델이 외부에 노출될 시 추후 도메인 모델 변경 할 때 도메인 모델에 의존하는 것들을 모두 변경해야 하지만, DTO를 사용하면 도메인 모델을 쉽게 변경할 수 있다.

## 7. 비즈니스 로직의 구현

* 비즈니스 로직은 Domain Model 계층에만 구현한다.

이유는 Service Layer는 다양한 Model을 읽어 제공하고, 복잡한 서비스는 더 많은 Model을 읽어 서비스를 제공하기 때문에 Service의 로직의 복잡도가 매우 높아지기 때문에, 트랜잭션과 도메인 간 순서보장의 기능만 하도록 구성해야 한다.

이렇게 복잡도를 낮춤으로써 유지보수와 테스트가 용이한 유연한 소프트웨어가 된다.