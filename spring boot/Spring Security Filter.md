## Spring Security Filter

스프링 시큐리티는 클라이언트의 모든 http요청에 대한 필터링을 통해 보안기능을 제공한다. 스프링 시큐리티의 필터링이 어떻게 구성되어 있는지 알아보자

#### 필터와 필터체인

서블릿 애플리케이션은 톰캣과 같은 서블릿 컨테이너 위에서 실행된다.

cilent의 요청이 발생했을 때 컨테이너의 작동방식은 다음과 같다.

1. client의 요청을 받고 요청의 uri를 통해 어떤 application에 요청을 전달해야 하는지 확인한다.
2. 컨테이너는 해당 app의 필터와 서블릿을 묶어 FilterChain을 구성하여 ServletRequest와 ServletResponse를 전달한다. 이때 서블릿은 모든 필터를 통해 요청이 필터링 되고 나서 요청을 전달받는다.
   * request와 response, FilterChain 객체를 전달받는다 -> 요청에 관련된 작업 후 FilterChain을 통해 다음 필터에 request, response를 넘겨준다.

```
public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain){  
    // 필터체인의 다음요소로 넘어가기전 작업들.. 
     
    chain.doFilter(request, response); // 필터체인의 다음요소로 넘긴다.

    // 필터체인의 마지막 요소들까지 요청이 전달된 후의 작업 
} 
```

#### DelegatingFilterProxy

스프링에서 제공하는 필터이다.

* 이 필터는 프록시 역할을 하여 필터 체인에 속하지 않은 객체를 필터처럼 작동 시킬 수 있도록 해준다.

이를 통해서 필터의 로직을 필터 체인 밖으로 꺼낼 수 있게 된다.

#### FilterChainProxy

스프링 시큐리티에서 사용하는 필터로, DelegatingFilterProxy와 같은 프록시 기능을 한다.

이 필터의 기능 및 의미는 다음과 같다

* 스프링 시큐리티 필터들의 시작점 역할을 한다.(시큐리티로서의 시작점 역할)
  * 애플리케이션의 다른 부분과 시큐리티 필터를 구분해 줄 수 있다.
  * 다른 시큐리티 필터에 넘어가기 전 전처리를 할 수 있다.
* 요청에 대한 SecurityFilterChain을 매칭 시켜서 전달할 수 있다. 여러개의 SecurityFilterChain중 uri로 매칭 시킨다.

#### SecurityFilterChain

스프링 시큐리티의 필터()들이 묶여있는 필터체인이다.

애플리케이셔에서 여러개의 SecurityFilterChain이 독립적으로 존재할 수 있으며, FilterChainProxy를 통해 요청에 매칭된다.

####보안 예외 처리

AccessDeniedException과 AuthenticationException은 security filter중 하나인 ExceptionTranslationFilter에서 처리한다.

* 이 필터는 자신의 다음순서의 필터중 예외가 발생한 경우를 캐치한다.

```
try { 
    filterChain.doFilter(request, response);  
} catch (AccessDeniedException | AuthenticationException ex) {  
    if (!authenticated || ex instanceof AuthenticationException) {  
        startAuthentication();  
    } else {  
        accessDenied();  
    }  
} 
```

1. 다음 필터들에 요청을 전달하고 예외발생시 캐치한다.
2. 인증과정의 문제 혹은 이증이 안 된 경우라면 인증을 하도록 한다.
3. 위 경우가 아닌 허가되지 않은 접근인 경우 해당하는 조치를 한다.

