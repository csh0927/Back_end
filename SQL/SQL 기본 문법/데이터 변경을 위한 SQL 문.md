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

```sql
CREATE TABLE 테이블_이름 (
	열_이름 타입 AUTO_INCREMENT PRIMARY KEY);
```

* 증가 되는 값을 지정하려면  시스템 변수인 `@@auto_increment_increment` 를 변경시켜야 한다.

```sql
CREATE TABLE 테이블_이름 (
	열_이름 타입 AUTO_INCREMENT PRIMARY KEY);
SET @@auto_increment_increment=증가값;
```

#### INSERT INTO ~ SELECT

다른 테이블에 이미 데이터가 입력되어 있다면 `INSERT INTO ~ SELECT` 구문을 사용해 해당 테이블의 데이터를 가져와서 한 번에 입력할 수 있다.

```sql
INSERT INTO 테이블_이름 (열_이름1, 열_이름2, ...)
	SELECT 문 ;
```

* 주의할 점은 SELECT 문의 열 개수는 INSERT할 테이블 열 개수와 같아야 한다.

### 데이터 수정 : UPDATE

행 데이터를 수정해야 하는 경우가 빈번하게 발생하는데, 이럴 때 UPDATE를 사용해서 내용을 수정한다.

```SQL
UPDATE 테이블_이름
	SET 열1=값1, 열2=값2, ...
	WHERE 조건 ;
```

* WHERE 절을 생략하면 테이블의 모든 행의 값이 변경된다. 주의 필요.

### 데이터 삭제 : DELETE

DELETE도 UPDATE와 거의 비슷하게 사용할 수 있다. DELETE는 행 단위로 삭제한다.

```sql
DELETE FROM 테이블이름 WHERE 조건 ;
```

* DELETE도 UPDATE와 마찬가지로 WHERE없이 사용하면 모든 행 데이터 삭제하니 주의

#### 대용량 테이블의 삭제

만약 몇억 건의 데이터가 있는 대용량의 테이블이 더 이상 필요 없다면 DROP으로 삭제하거나, 테이블의 구조를 남겨놓고 싶다면 TRUNCATE로 삭제하는 것이 효율적이다.

|             용어             |  약자  | 설명                                       |
| :------------------------: | :--: | ---------------------------------------- |
|            NULL            |      | 아무것도 없는 값. AUTO_INCREMENT 열에 값을 입력할 때는 NULL로 지정함 |
|        PRIMARY KEY         |  PK  | 기본 키, AUTO_INCREMENT 열은 기본 키로 지정해야 함     |
|        ALTER TABLE         |      | 테이블의 구조를 변형하는 SQL                        |
|           시스템 변수           |      | MySQL에서 자체적으로 가지고 있는 설정값이 저장된 변수         |
| @@auto_increment_increment |      | AUTO_INCREMENT의 증가값을 지정하는 시스템 변수         |
|          DESCRIBE          | DESC | 테이블의 구조를 확인하는 SQL                        |
|          TRUNCATE          |      | DELETE와 비슷한 기능이지만 전체 행을 삭제할 때 사용         |

