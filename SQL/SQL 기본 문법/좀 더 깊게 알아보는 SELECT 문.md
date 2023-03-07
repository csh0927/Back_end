## 좀 더 깊게 알아보는 SELECT 문

### ORDER BY 절

order by 절은 결과의 값이나 개수에 대해서는 영향을 미치지 않지만, 결과가 출력되는 순서를 조절한다.

```sql
SELECT 열_이름
	
	FROM 테이블_이름
	
	ORDER BY 열_이름;                                                                    
```

기본값은 오름차순인 ASC 인데 Ascending의 약자로 오름차순을 의미하고, DESC는 Descending의 약자로 내림차순을 의미한다.

* ORDER BY 절과 WHERE 절을 함께 사용할 수 있다.

#### LIMIT

LIMIT은 출력의 개수를 제한한다. (ex: 테이블을 조회하는데 전체 중 앞에서 원하는 몇 건만 조회할 수 있다.)

```sql
SELECT 열_이름

	FROM 테이블_이름
	
	ORDER BY 열_이름
	
	LIMIT 숫자;
```

* 주로 ORDER BY와 함께 사용한다.
* 숫자를 콤마로 구분하여 쓰면 첫번째 수 부터 두번째 수 건만 조회할 수 있다. (ex: LIMIT 3, 2 라 쓰면 3번째부터 2건만 조회할 수 있다.)

#### DISTINCT

DISTINCT는 조회된 결과에서 중복된 데이터를 1개만 남긴다.

```sql
SELECT DISTINCT 열_이름 FROM 테이블_이름;
```

### GROUP BY 절

GROUP BY 절은 말 그대로 그룹으로 묶어주는 역할을 한다.

GROUP BY와 함께 사용되는 집계 함수

|       함수명       | 설명                     |
| :-------------: | ---------------------- |
|      SUM()      | 합계를 구한다.               |
|      AVG()      | 평균을 구한다.               |
|      MIN()      | 최소값을 구한다.              |
|      MAX()      | 최대값을 구한다.              |
|     COUNT()     | 행의 개수를 센다.             |
| COUNT(DISTINCT) | 행의 개수를 센다.(중복은 1개만 인정) |

### Having 절

GROUP BY 절에 WHERE 절을 사용하려 하면 오류가 난다. 그렇기에 Having 절을 사용해야 한다.

```sql
SELECT 열_이름

	FROM 테이블_이름
	
	GROUP BY 열_이름
	
	HAVING 조건식;
```

HAVING 절은 꼭 GROUP BY 절 다음에 나와야 한다.