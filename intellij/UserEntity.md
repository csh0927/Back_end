```
package com.example.logincode_annotation.Entity;

import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Getter;
import lombok.NoArgsConstructor;

import javax.persistence.Column;
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import javax.persistence.Table;


@Entity //테이블에 대응하는 하나의 클래스라고 생각하면 편하다. 때로는 클래스를 의미하는 경우도 있고, 클래스에 의해 생성된 인스턴스를 의미하는 경우가 있다.
@Getter //객체 외부에서 객체 필드값을 사용하기 부적절한 경우일 때,
메소드로 필드값을 가공후 외부로 전달한다.
@Builder //필요한 데이터만 설정할 수 있고 유연성을 확보할 수 있다. 
    그리고 가독성을 높일 수 있으며, 변경 가능성을 최소화할 수 있다.
@AllArgsConstructor //모든 필드 값을 파라미터로 받는 생성자를 만든다.
@NoArgsConstructor //파라미터가 없는 기본 생성자를 생성해준다.
@Table(name = "user") //맵핑할 테이블을 지정하고 name은 매핑할 테이블의 이름을 지정한다.
public class UserEntity {

    @Id //JPA가 객체를 관리할 때 식별할 기본키를 지정한다.
    @GeneratedValue(strategy = GenerationType.IDENTITY) //주키의 값을 위한 자동 생성 전략을 명시하는데 사용한다. strategy는 엔티티의 주키를 생성할 때 사용해야 하는 주키생성 전략을 의미한다.
    private Long id;

    @Column(nullable = false) //객체 필드와 DB 테이블 컬럼을 맵핑하고 nullable은 NULL을 허용할지, 허용하지 않을지 결정한다.
    private String name;

    @Column(nullable = false)
    private String pwd;


}
```