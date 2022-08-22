### @NoArgsConstructor

@NoArgsConstructor은 파라미터(매개변수)가 없는 기본 생성자를 생성해준다.

### @AllArgsConstructor

@AllArgsConstructor은 모든 필드값을 파라미터(매개변수)로 받는 생성자를 생성해준다.

### @RequiredArgsConstructor

@RequiredArgsConstructor은 초기화 되지 않은 final 필드나, @NonNull이 붙은 필드에 대해 생성자를 생성해준다. 주로 의존성 주입 편의성을 위해서 사용되곤 한다. 사용하면 필드에 final 키워드를 사용 가능하고 순환 참조를 방지할 수 있으며 결합도가 낮아서 테스트가 쉽다. (@Autowired 대신 사용한다.)

```
@NoArgsConstructor
@RequiredArgsConstructor
@AllArgsConstructor
public class User {
  private Long id;
  @NonNull
  private String username;
  @NonNull
  private String password;
  private int[] scores;
}
```

