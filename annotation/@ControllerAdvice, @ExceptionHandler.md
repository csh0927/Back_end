## @ControllerAdvice

* @Controller 와 @RestController 어노테이션이 있는 모든 곳에서의 예외를 잡을 수 있도록 해준다.

* @RestControllerAdvice는 @ControllerAdvice에 @ResponseBody를 합쳐놓은 어노테이션으로, @ControllerAdvice와 동일한 역할을 수행하고, 추가적으로 객체를 리턴할 수도 있다.

* 위 두 어노테이션 모두 적용 범위를 클래스나 패키지 단위로 제한할 수도 있으며, 아래와 같이 사용하면 된다.

  ```
  @RestControllerAdvice(basePackageClasses = EditController.class)
  ```

  ```
  @RestControllerAdvice(basePackages = "com.app.edit.controller")
  ```

## @ExceptionHandler

컨트롤러 내 특정 Exception을 처리하기 위한 어노테이션이다. 이 어노테이션을 메서드에 선언하고 특정 예외 클래스를 지정해주면 해당 예외가 발생했을 때 메서드에 정의한 로직으로 처리할 수 있다. 

@Controller 클래스 내에서도 사용 가능하다. 하지만 Exception들을 전역적으로 처리하기 위해, 대부분 @ControllerAdvice 클래스에서 활용된다.

```
@ControllerAdvice
public class ControllerAdvice {

    @ExceptionHandler(CustomException.class)
    public ResponseEntity<String> handleCustomException() {
        ...
    }
}
```
