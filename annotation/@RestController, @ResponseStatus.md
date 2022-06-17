### @RestController

@RestController는 @Controller에 @ResponseBody가 결합된 어노테이션이다. 컨트롤러 클래스에 @RestController를 붙이면, 컨트롤러 클래스 하위 메소드에 @ResponseBody 어노테이션을 붙이지 않아도 문자열과 JSON 등을 전송할 수 있다.

```
@RestController
@RequestMapping("/hello/*")
public class RestController {
    
    @RequestMapping("/test")
    public String test() {
        return "test";
    }
}
```

### @ResponseStatus

@ResponseStatus는 HTTP 상태를 변경하도록 도와주는 어노테이션이다.

```
@ResponseStatus(value = HttpStatus.NOT_FOUND)
public class NoSuchElementFoundException extends RuntimeException {
  ...
}
```

