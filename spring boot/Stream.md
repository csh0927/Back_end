# Stream

스트림을 이용하면 선언형으로 기존의 컬렉션 데이터들을 처리할 수 있게된다. 쉽게 생각하면 컬렉션 반복을 좀 더 효율적이고 간편하게 수행할 수 있는 방법이라고 볼 수 있다. 또한 데이터 병렬 처리에도 용이한 장점이 있다.

자바에서 스트림을 쉽게 이해하기 위해 예를 들면 물고기가 그물에 걸러지고 일정한 규격으로 포장한 뒤 소비자에게 전달되는 것이다.

흐름속을 헤엄쳐 다니는 물고기와 해양 생물들은 컬렉션 데이터라 할 수 있다. 데이터들은 스트림을 유영하다가 그물에 걸러진다. 코드에서는 `filter` 로 표현 되는 부분이다. `filter` 에 걸러진 데이터들은 이제 일정한 규격으로 포장이 되게 되는데 코드에서는 `map` 으로 표현된다. 그리고 마지막으로 소비자에게 배달 되는 것이 collect라고 할 수 있다.

* 물결이 한 번 흐르고 나면 다시 되돌아 올 수 없듯, 스트림 역시 한 번만 소비할 수 있다.

**장점**
스트림을 활용하게 되면 선언저긍로 코드를 구현할 수 있기 때문에 일정부분 코드의 가독성이 올라간다. 또 `filter, map, sorted, collect` 등과 같은 다양한 빌딩 블록 연산을 통해 다양한 파이프라인을 구성할 수 있다. 그리고 이런 연산 블록들은 병렬연산에 자유롭기 때문에 병렬화를 통해 성능을 향상시킬 수 있다.

* 병렬화란 순차적인 직렬 프로그램을 분할하고 분할된 단위를 동시에 병렬로 수행함으로써 성능을 향상시키는 프로그래밍 기술이다.

**컬렉션과 스트림**

* 컬렉션은 현재 자료구조에 포함된 모든 값을 계산한 다음에 컬렉션에 추가할 수있다.(적극적 생성, 모든 값을 계산할 때까지 기다린다.)
* 스트림은 필요할 때 값을 계산한다.(게으른 생성, 필요할 때만 값을 계산한다는 의미이다.)

비유를 해보면 컬렉션은 팔기도 전에 창고를 가득 채우며 적극적 생산하고 스트림은 요청하는 값만 스트림에서 추출한다.

컬렉션은 데이터를 반복해서 사용할 수 있고 스트림은 데이터를 단 한번만 소비할 수 있다.

*************************************

코드로 공부해보기

```
//스트림 생성
List<String> list = Arrays.asList("a", "b", "c");
Stream<String> stream = list.stream();

//빌더 생성
String<String> stream = Stream<String>builder()
				.add("a")
				.add("b")
				.add("c")
				.build();
							
//필터
Stream<T> filter(Predicate<? super T> predicate);
//filter() 메소드에는 boolean 값을 리턴하는 람다식을 넘겨주게 된다. 뽑아져 나오는 데이터에 대해 람다식을 적용해서 true가 리턴되는 데이터만 선별한다.

//예제
Stream<Integer> stream = IntStream.range(1, 10).boxed();
stream.filter(v -> ((v % 2) == 0))
		.forEach(System.out::println);
//2, 4, 6, 8 짝수 객체만 뽑아내는 필터 예제

//Map
//map()은 스트림에서 뽑아져 나오는 데이터에 변경을 가해준다.
<R> Stream<R> map(Function<? super T, ? extends R> mapper);

//map() 메소드는 값을 변환해주는 람다식을 인자로 받는다. map() 메소드의 인자로 받은 람다식을 적용해 새로운 데이터를 만들어낸다.

Stream<Integer> stream = IntStream.range(1, 10).boxed();
stream.filter(v -> ((v % 2) == 0))
		.map(v -> v % 10)
		.forEach(System.out::println);
//20, 40, 60, 80 짝수만 뽑아 낸 다음 곱하기 10을 해서 새로운 숫자를 생성하는 스트림 예제

//Map과 비슷한 flatMap
<R> Stream<R> flatMap(Function<? super T, ? extends Stream<? extends R>> mapper);

//flatMap() 메소드의 인자로 받는 람다는 리턴 타입이 Stream이다. 즉, 새로운 스트림을 생성해서 리텅하는 람다를 인자로 받는다. 플랫트닝을 하는 역할
//플랫트닝(Flattenning) : 중첩 된 스트림 구조를 한단계 적은 단일 컬렉션에 대한 스트림으로 만들어주는 작업

//예제
List<List<String>> list = Arrays.asLists(Arrays.asList("A", "B", "C"), Arrays.asList("a", "b", "c"));
List<String> flatList = list.stream()
				.flatMap(Collection::stream)
				.collect(Collection::toList());
// [["A", "B", "C"], ["a", "b", "c"]] -> ["A", "B", "C", "a", "b", "c"]
//(e) -> Collection.stream(e) 이를 축약해서 Collection::stream

//스트림 데이터들을 정렬하고자할 때는 sorted() 메소드를 이용, 오름차순 정렬

//Peek() 메소드는 스트림 내 원소들을 대상으로 map() 메소드처럼 연산을 수행한다. 그냥 인자로 받은 람다를 적용하기만 한다.

Stream<T> peek(Consumer<? super T> action);

//예제
int sum = IntStream.range(1, 10)
	.peek(System.out::println)
	.sum();
//이런식으로 중간에 로깅 같은 것을 하고자 할 때, peek() 메소드를 사용하면 좋다.

//지금까지 본 데이터 수정 연산들은 데이터에 수정을 가한 결과 데이터들을 만들어내는 또 다른 스트림 객체를 리턴했다. 즉, 중간 작업(Intermediate Operations)들이며 이들만으로는 의미있는 스트림을 만들 수 없다. 데이터 가공, 필터링한 다음 출력하거나, 컬렉션으로 모아두는 등의 작업이 필요하다.

//Reduce
중간 연산을 거친 값들은 reduce라는 메소드를 이용해 결과값을 만들어낸다. reduce() 메소드는 파라미터에 따라 3가지 종류가 있다.

//스트림에서 나오는 값들을 accumulator 함수로 누적
Optional<T> reduce(BinaryOperator<T> accumulator);

//동일하게 accumulator 함수로 누적하지만 초기값(identity)이 있음
T reduce(T identity, BinaryOperator<T> accumulator);

Set<Integer> evenNumber = IntStream.range(1, 1000).boxed()
					.filter(n -> (n % 2 == 0))
					.collect(Collectors.toSet());
								
//Collector.joining()을 사용하면 작업한 결과를 하나의 문자열로 이어 붙이게 된다.

List<String> hi = Arrays.asList("dks", "sud", "gk");
String returnValue = hi.stream()
				.collect(Collectors.joining());

System.out.println(returnValue);
//dkssudgk

//스트림에서 뽑아져 나오는 값에 대해서 어떤 작업을 하고 싶을 때 foreach 메소드를 사용한다. 이 메소드는 앞에서 본 메소드들과 다르게 어떤 값을 리턴하지는 않는다.

Set<Integer> evenNumber = IntStream.range(1, 1000).boxed()
					.filter(n -> (n % 2 == 0))
					.forEach(System.out::println);
```