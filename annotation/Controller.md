

```
package com.example.logincode_annotation.Controller;

// class
import com.example.logincode_annotation.Dto.UserDto;
import com.example.logincode_annotation.Service.UserService;

// lombok
import lombok.RequiredArgsConstructor;

import org.springframework.http.HttpStatus;

// 어노테이션
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.ResponseStatus;
import org.springframework.web.bind.annotation.RestController;

// validation
import javax.validation.Valid;

@RequiredArgsConstructor //final필드와 @NonNull어노테이션이 붙은 필드에 대한 생성자를 생성하여
특정 변수만을 활용하는 생성자를 생성해준다.
@RestController //Json 형태로 객체 데이터를 반환한다. 최근의 데이터를 응답으로 제공하는 REST API를 개발할 때 주로 사용하며 ResponseEntity로 감싸서 반환한다.
public class Controller {

    private final UserService userService;

    @PostMapping("/join") //HTTP 전송 방식의 타입이고 캐시가 남지 않아 보안적인 면에서 좋고 요청 시 Request Body에 데이터가 들어가기 때문에 파라미터가 노출되지 않는다.
    @ResponseStatus(HttpStatus.CREATED) //Controller나 Exception에 사용하여 status 정보를 설정하여 리턴해 준다.
    public void join(@RequestBody @Valid UserDto userDto) {userService.saveData(userDto);
    /*클라이언트에서 서버로 요청 메세지를 보낼 때, 
    본문에 데이터를 담아서 보내야 하고, 서버에서 클라이언트로 응답을 보낼 때에도 본문에 데이터를 담아서 보내야 한다. 
    이 본문이 바로 body이다. 즉 요청본문 RequestBody, 응답본문 ResponseBody를 담아서 보내야 한다.
    또 파라미터로 @RequestBody 어노테이션 옆에 @valid를 작성하면 RequestBody로 들어오는 객체에 대한 검증을 수행한다.*/
    }

    @PostMapping("/login")
    @ResponseStatus(HttpStatus.CREATED)
    public UserDto login(@RequestBody @Valid UserDto userDto) {
        return userService.login(userDto);
    }

    @GetMapping("/login/{name}/exists") //SELECT 기능면에서 우수하여 이 기능으로 많이 쓰고 캐시가 남아있어 보안적인 측면이 좋지 않으나, 전송속도가 우수하고 파라미터가 url에 노출되는 점이 있다.
    @ResponseStatus(HttpStatus.OK)
    private void exists(@PathVariable String name) { //PathVariable은 url에서 각 구분자에 들어오는 값을 처리해야 할 때 사용한다.
        userService.exists(name);
    }


}

```
