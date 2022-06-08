### Mapping annotation

@RequestMapping : 요청에 대해 어떤 Controller, 어떤 메소드가 처리할지를 맵핑하기 위한 어노테이션
@GetMapping : Get 요청을 하는 API의 어노테이션, 데이터를 가져올 때 사용한다.
@PostMapping : POST 요청을 하는 API의 어노테이션, 데이터를 게시할 때 사용한다.
@PutMapping : PUT 요청을 하는 API의 어노테이션, 데이터를 수정할 때 사용한다.
@DeleteMapping : DELETE 요청을 하는 API의 어노테이션, 데이터를 삭제할 때 사용한다.
@PatchMapping : PATCH 요청을 하는 API의 어노테이션, 데이터를 수정할 때 사용한다.

### @RequestMapping 대신 Post나 Get을 사용하는 이유

@RequestMapping 대신 Post, Get을 쓰면 코드를 짧게 줄일 수 있고 어떤 HttpMethods로 맵핑시킬지도 명확하기 때문에 Post나 Get을 쓴다.

### Get, Post 차이점

@GetMapping은 URL에 변수를 포함시켜 요청하고 URL에 데이터가 노출되어 보안에 취약하지만 @PostMapping은 URL에 변수를 노출하지 않고 요청을 하고 URL에 데이터가 노출되지 않아서 기본 보안이 설정되어 있다.

### Patch, Put 차이점

@PatchMapping은 지정된 정보만 수정하는 반면 @PutMapping은 전제 정보를 수정하는 것이다.

