## Token 기반 인증 시스템

토큰 기반 인증 시스템은 인증받은 사용자들에게 토큰을 발급하고, 서버에 요청을 할 때 헤더에 토큰을 함께 보내도록 하여 유효성 검사를 한다. 이러한 시스템에서는 더이상 사용자의 인증 정보를 서버나 세션에 유지하지 않고 클라이언트 측에서 들어오는 요청만으로 작업을 처리한다.

**토큰 기반 인증 시스템의 작동 과정**

1. 사용자가 아이디와 비밀번호로 로그인을 한다.
2. 서버 측에서 해당 정보를 검증한다.
3. 정보가 정확하다면 서버 측에서 사용자에게 Signed 토큰을 발급한다. (Signed는 해당 토큰이 서버에서 정상적으로 발급된 토큰임을 증명하는 Signature를 가지고 있다는 것)
4. 클라이언트 측에서 전달받은 토큰을 저장해두고, 서버에 요청을 할 때마다 해당 토큰을 서버에 함께 전달한다. 이때 Http 요청 헤더에 토큰을 포함시킨다.
5. 서버는 토큰을 검증하고, 요청에 응답한다.

**토큰 기반 인증 시스템의 이점**

1. 무상태성, 확장성

   토큰은 클라이언트 측에 저장되기 때문에 서버는 완전히 Stateless 하며, 클라이언트와 서버의 연결고리가 없기 때문에 확장하기에 매우 적합하다. 만약 사용자 정보가 서버 측 세션에 저장된 경우에 서버를 확장하여 분산처리를 한다면, 해당 사용자는 처음 로그인 했었던 서버에만 요청을 받도록 설정을 해주어야 한다. 하지만 토큰을 사용한다면 어떠한 서버로 요청이 와도 상관이 없다.

2. 여러 플랫폼 및 도메인

   서버 기반 인증 시스템의 문제점 중 하나인 CORS를 해결할 수 있다. 토큰을 사용한다면 어떤 디바이스, 어떤 도메인에서도 토큰의 유효성 검사를 진행한 후에 요청을 처리할 수 있다.

