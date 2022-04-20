```
package com.example.logincode_annotation.Dto;

import lombok.Builder;
import lombok.Getter;
import lombok.NoArgsConstructor;

import javax.validation.constraints.NotBlank;

@Getter //객체 외부에서 객체 필드값을 사용하기 부적절한 경우가 있다. 이런 경우 메소드로 필드값을 가공후 외부로 전달하는데, 이런 역할을 하는 메소드가 Getter이다.
@NoArgsConstructor //파라미터가 없는 기본 생성자를 생성해준다.
public class UserDto {

    @NotBlank //null과 "", " " 모두 허용하지 않고 가장 강도가 높다.
    private String name;

    @NotBlank
    private String pwd;

    @Builder //필요한 데이터만 설정할 수 있고 유연성을 확보할 수 있다. 그리고 가독성을 높일 수 있으며, 변경 가능성을 최소화할 수 있다.
    public UserDto(String name, String pwd) {
        this.name = name;
        this.pwd = pwd;
    }

}
```