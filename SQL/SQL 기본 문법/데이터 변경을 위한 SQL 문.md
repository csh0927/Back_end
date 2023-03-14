## 데이터 변경을 위한 SQL 문

### 데이터 입력: INSERT

#### INSERT 기본 문법

테이블에 행 데이터를 입력하는 기본적인 SQL 문은 INSERT입니다.

```sql
INSERT INTO 테이블 [(열1, 열2, ...)] VALUES (값1, 값2, ...)
```

테이블 이름 다음에 나오는 열은 생략이 가능하다. 열 이름을 생략할 경우에 VALUES 다음에 나오는 값들의 순서 및 개수는 테이블을 정의할 때의 열 순서 및 개수와 동일해야 한다.

#### 자동으로 증가하는 AUTO_INCREMENT

AUTO_INCREMENT는 열을 정의할 때 1부터 증가하는 값을 입력해줍니다. INSERT에서는 해당 열이 없다고 생각하고 입력하면 된다. 단 주의할 점은 AUTO_INCREMENT로 지정하는 열은 꼭 PRIMARY KEY로 지정해줘야 한다.



