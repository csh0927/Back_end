# @Slf4j

**Slf4j**

* 로깅을 간단하게 사용할 수 있도록 하는 Facade (로깅 : 시스템 동작 시 시스템 상태/작동 정보를 시간의 경과에 따라 기록하는 것을 로깅이라고 한다.)
* 로깅 라이브러리들을 하나의 통일된 방식으로 사용할 수 있는 방법이다.

**Slf4j(Simple Logging Facade for Java) **란?

* java.util.logging, logback, log4j 와 같은 다양한 로깅 프레임 워크에 대한 추상화 역할을 하는 라이브러리이다.
* 추상 로깅 프레임워크 이기에 단독 사용은 하지 않는다.
* compile 시 하나의 로깅 프레임워크와 바인딩 해준다.

Slf4j의 이점

* 로깅 프레임워크를 라이브러리만 추가해서 바인딩 할 수 있다.

**로그 레벨**

* `` TRACE < DEBUG < INFO < WARN < ERROR``
* 레벨에 따라서 로그 메세지가 달라진다.
* TRACE: 추적 레벨은 DEBUG보다 좀 더 상세한 정보를 표시한다.
* DEBUG: 프로그램을 디버깅하기 위한 정보를 표시한다.
* INFO: 상태 변경과 같은 정보성 로그를 표시한다.
* WARN: 처리 가능한 문제, 시스템 에러의 원인이 될 수 있는 경고성 메시지를 표시한다.
* ERROR: 요청을 처리하는 중 오류가 발생한 경우를 표시한다.


**로그 사용법**

```
@Controller
@Slf4j
public class TestController {
    @GetMapping("/")
    public String String(String str){
        try {
            str.toString();
        } catch (NullPointerException e){
            log.trace("가장 디테일한 로그");
            log.warn("경고");
            log.info("정보성 로그");
            log.debug("디버깅용 로그");
            log.error("에러",e);
        }
        return "test";
    }
}
```

로깅이 필요한 부분에는 log 변수로 로그를 생성하면 된다.