# 토큰의 구성요소

JWT는 .을 기준으로 헤더(header) - 내용(payload) - 서명(signature)

**aaaaaa.bbbbbb.cccccc**
header payload signature

* **Header**
  * `typ` : 토큰의 타입을 지정한다. JWT라는 문자열이 들어가게 된다.
  * `alg` : Signature 를 해싱하기 위한 알고리즘을 지정합니다.
* **Payload**
  토큰에 담을 정보가 들어간다. **정보의 한 덩어리를 클레임(claim)**이라고 부르며, key-value의 한 쌍으로 이루어져 있다. 클레임의 종류는 세 종류로 나눌 수 있다.
  * **등록된(registered) 클레임**
    토큰에 대한 정보를 담기 위한 클레임들이며, 이미 이름이 등록되어있는 클레임
    * `iss` : 토큰 발급자(issuer)
    * `sub` : 토큰 제목(subject)
    * `aud` : 토큰 대상자(audience)
    * `iat` : 토큰이 발급된 시간(issued at)
    * `exp` : 토큰의 만료시간(expiration). 시간은 NumericDate 형식이다. (예 : 1480129381232)
    * `nbf` : 토큰의 활성 날짜(Not Before). NumericDate 형식으로 날짜를 지정하며, 이 날짜가 지나기 전까지는 토큰이 처리되지 않는다.
    * `jti` : JWT의 고유 식별자로서, 주로 일회용 토큰에 사용한다.
  * **공개(public) 클레임**
    말 그대로 공개된 클레임, 충돌을 방지할 수 있는 이름을 가져야하며, 보통 클레임 이름을 URI로 짓는다.
  * **비공개(private) 클레임**
    클라이언트 - 서버간의 통신을 위해 사용되는 클레임
* **Signature**
  * 서버에서 토큰이 유효한지 검증하기 위한 문자열
  * Header 인코딩 + Payload 인코딩한 값을 Secret Key를 통해 해쉬값을 생성하므로 데이터 변조 여부를 판단 가능하다.
  * Secret Key는 노출되지 않도록 서버에서 잘 관리해야 한다.

