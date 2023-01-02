## Optional

#### NPE란?

개발을 할 때 많이 발생하는 예외 중 하나가 바로 NPE(NullPointerException)이다. NPE를 피하려면 null 여부를 검사해야 하는데, null 검사를 해야하는 변수가 많은 경우 코드가 복잡해지고 번거롭다. 그래서 null 대신 초기값을 사용하길 권장하기도 한다.

#### Optional이란?

Java8 부터는 Optional<T> 클래스를 사용해 NPE를 방지할 수 있도록 도와준다. **Optional<T>는 null이 올 수 있는 값을 감싸는 Wrapper 클래스**로, 참조하더라도 NPE가 발생하지 않도록 도와준다. Optional 클래스는 아래와 같은 value에 값을 저장하기 때문에 값이 null이더라도 바로 NPE가 발생하지 않으며, 클래스이기 때문에 각종 메소드를 제공해준다.

* Optional.of - 값이 Null이 아닌 경우
  * 만약 어떤 데이터가 절대 null이 아니라면 Optional.of()로 생성할 수 있다. 만약 Optional.of()로 Null을 저장하려고 하면 NullPointerException이 발생한다.
* Optional.ofNullbale() - 값이 Null일 수도, 아닐 수도 있는 경우
  * 만약 어떤 데이터가 null이 올 수도 있고 아닐 수도 있는 경우에는 Optional.ofNullbale로 생성할 수 있다. 그리고 이후에 orElse 또는 orElseGet 메소드를 이용해서 값이 없는 경우라도 안전하게 값을 가져올 수 있다.