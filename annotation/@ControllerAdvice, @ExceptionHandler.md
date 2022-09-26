# 예외 처리

## @ControllerAdvice

Try-catch문 보다 발생하는 예외를 체계적으로 관리할 수 있는 예외처리 방법, @Controller 와 @RestController 어노테이션이 있는 모든 곳에서의 예외를 잡을 수 있도록 해줍니다.

- RestController는 Controller + ResponseBody 이고 ResponseBody는 JSON으로 본문을 반환해줍니다.
- Try-catch는

```
 try {
//예외가 발생할 가능성이 있는 문장
}catch(Exception e1) {
//예외가 발생했을 경우, 이를 처리하기 위한 문장을 넣는다.
}

```

요런식으로 예외를 처리하는 것.

## @ExceptionHandler

컨트롤러 내 특정 Exception을 처리하기 위한 어노테이션입니다. @Controller 클래스 내에서도 사용 가능합니다. 하지만 Exception들을 전역적으로 처리하기 위해, 대부분 @ControllerAdvice 클래스에서 활용됩니다.

```
@ControllerAdvice
public class ControllerAdvice {

    @ExceptionHandler(CustomException.class)
    public ResponseEntity<String> handleCustomException() {
        // ...
    }
}

```

만약 ExceptionHandler가 없다면 try-catch 문으로 처리하거나 throw 해야 하기 때문에 중복되는 코드가 많아져서 @ExceptionHandler를 사용하여 공통 로직에서 처리하면 편리합니다.