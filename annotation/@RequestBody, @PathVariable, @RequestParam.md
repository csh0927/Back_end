### @RequestBody

@RequestBody가 붙은 파라미터(매개변수)에는 http요청의 본문(body)이 그대로 전달된다. json기반의 메시지를 사용하는 요청의 경우 이 방법이 유용하다.

```
@RequestMapping(value = "/ajaxTest.do")
public String ajaxTest(@RequestBody UserVO getUserVO) throws Exception {
    ...
}
```

### @PathVariable

매핑의 URL에 { } 로 들어가는 패스 변수(path variable)를 받는다.

```@GetMapping("/board/{seq}")
@GetMapping("/board/{num}")
public String save(@PathVariable int num){
    ...
}
```

### @RequestParam

@RequestParam은 URL에서 파라미터(매개변수)값과 이름을 함께 전달하는 방식으로 게시판 등에서 페이지 및 검색 정보를 함께 전달하는 방식을 사용할 때 많이 사용한다. 주로 GET 방식의 통신을 할 때 많이 사용한다.

```
@GetMapping("/board")
public String save(@RequestParam("num") int num){
    ...
}
```

### 쿼리스트링

쿼리스트링으로 파라미터를 URL로 전송할 때엔 컨드롤러에서 파라미터를 받을때 @RequestParam을 사용한다.

```
@RestController
@RequiredArgsConstructor
public class MembeController {
  private final MemberService memberService
  
  @GetMapping("/member")
  public List<MemberVO> getMemberById(@RequestParam Long id){
    return memberService.selectMemberById(id)
  }
}
```

```
GET http://localhost:8080/member?id=2
```

@RequestParam 어노테이션을 컨트롤러 파라미터에 작성하면 쿼리 스트링으로 들어오는 영역에서 id값을 매핑해서 가져올 수 있다.