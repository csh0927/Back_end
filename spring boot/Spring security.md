# Spring security

* Spring 기반의 애플리케이션의 보안(인증과 권한, 인가 등)을 담당하는 스프링 하위 프레임워크.

  인증과 권한에 대한 부분을 Filter 흐름에 따라 처리한다. Filter는 Dispatcher Servlet으로 가기 전에 적용되므로 가장 먼저 URL 요청을 받지만, Interceptor는 Dispatcher와 Controller 사이에 위치한다는 점에서 적용 시기의 차이가 있다. Spring security는 보안과 관련해서 체계적으로 많은 옵션을 제공해주기 때문에 개발자 입장에서는 일일이 보안 관련 로직을 작성하지 않아도 된다는 장점이 있다.

### 인증 & 인가

* 인증(Authentication) : 해당 사용자가 본인이 맞는지를 확인하는 절차
* 인가(Authorization) : 인증된 사용자가 요청한 자원에 접근 가능한지를 결정하는 절차

**인증 ---------------------> 인가**(인증 성공 후)

Spring security는 기본적으로 인증 절차를 거친 후에 인가 절차를 진행하게 되며, 인가 과정에서 해당 리소스에 대한 접근 권한이 있는지를 확인하게 된다. Spring security에서는 이러한 인증과 인가를 위해 Principal을 아이디로, Credential을 비밀번호로 사용하는 Credential 기반의 인증 방식을 사용한다.

* 접근 주체(Principal) : 보호받는 Resource에 접근하는 대상


* 비밀번호 (Credential) : Resource에 접근하는 대상의 비밀번호

### 구현에 필요한 구체적인 개념

#### SecurityContextHolder

보안 주체의 세부 정보를 포함하여 응용프로그램의 현재 보안 컨텍스트에 대한 세부 정보가 저장된다. 기본적으로 SecurityContextHolder.MODE_INHERITABLETHREADLOCAL 방법과SecururityContextHolder.MODE_THREADLOCAL 방법을 제공한다.

#### SecurityContext

Authentication을 보관하는 역할을 하며, SecurityContext를 통해 Authentication 객체를 꺼내올 수 있다.

#### Authentication

현재 겁근하는 주체의 정보와 권한을 담는 인터페이스이다. Authentication객체는 SecurityContext에 저장되며, SecurityContextHolder를 통해 SecurityContext에 접근하고, SecurityContext를 통해 Authentication에 접근할 수 있다.

#### UsernamePasswordAuthenticaionToken

Authentication을 implements한 AbstractAuthenticationToken의 하위 클래스로, User의 ID가 Principal 역할을 하고, Password가 Credential의 역할을 한다.

#### Authentication Manager

인증에 대한 부분은 SpringSecurity의 AuthenticationManager를 통해서 처리하게 되는데, 실질적으로는 AuthenticationManager에 등록된 AuthenticationProvider에 의해 처리된다. 인증이 성공하면 인증이 성공한 객체를 생성하여 SecurityContext에 저장한다.

#### UserDetails

인증이 성공하여 생성된 UserDetails 객체는 Authentication 객체를 구현한UsernamePasswordAuthenticationToken을 생성하기 위해 사용된다.

#### UserDetailsService

UserDetailsService 인터페이스는 UserDetails 객체를 반환하는 단 하나의 메소드를 가지고 있는데, 일반적으로 이를 구현한 클래스 내부에 UserRepository를 주입받아 DB와 연결하여 처리한다.

#### PasswordEncoding

AuthenticationManagerBuilder.userDetailsService().passwordEncoder()를 통해 패스워드 암호화에 사용될 PasswordEncoder 구현체를 지정할 수 있다.

#### GrantedAuthority

현재 사용자가 가지고 있는 권한을 의미한다. ROLE_ADMIN이나 ROLE_USER와 같이 ROLE_* 형태로 사용하며, 보통 "roles" 라고 한다. GrantedAuthority 객체는 UserDetailsService에 의해 불러올 수 있고, 특정 자원에 대한 권한이 있는지를 검사하여 접근 허용 여부를 결정한다.