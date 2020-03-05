## SQL Join

**조인이란**

- 두 개 이상의 테이블이나 데이터베이스를 연결하여 데이터를 검색하는 방법을 말한다.
- 테이블을 연결하려면, 적어도 하나의 칼럼을 서로 공유하고 있어야 하므로 이를 이용하여 데이터 검색에 활용한다.



### Join 종류

- INNER JOIN
- LEFT OUTER JOIN
- RIGHT OUTER JOIN
- FULL OUTER JOIN
- CROSS JOIN
- SELF JOIN

```sql
문법
SELECT
테이블별칭.조회할컬럼,
테이블별칭.조회할컬럼
FROM 기준테이블 별칭
INNER JOIN 조인테이블 별칭 ON 기준테이블별칭.기준키 = 조인테이블별칭.기준키 ...
```



**1) INNER JOIN**

<img src="https://user-images.githubusercontent.com/33534771/75853566-c1706b00-5e31-11ea-83bc-1e2ebe4d9f61.png" />

- 쉽게 말해 **교집합**이라고 생각하면 된다.
- 기준 테이블과 Join한 테이블의 **중복된 값**을 보여준다.
- 결과값은 A의 테이블과 B 테이블이 모두 가지고 있는 데이터만 검색된다.

```sql
Ex)
SELECT
A.NAME, 
B.AGE
FROM EX_TABLE A
INNER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```



**2) LEFT OUTER JOIN**

<img src="https://user-images.githubusercontent.com/33534771/75853627-e238c080-5e31-11ea-89bb-a5afe1058cfd.png" />

- **기준 테이블의 값 + 테이블과 기준테이블의 중복된 값**을 보여준다.
- 왼쪽 테이블을 기준으로 Join을 하겠다고 생각하면 된다.
- 결과값은 A 테이블의 모든 값과 A 테이블과 B 테이블의 중복되는 값이 검색된다.

```sql
SELECT
A.NAME,
B.AGE
FROM EX_TABLE A
LEFT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```



**3) RIGHT OUTER JOIN**

<img src="https://user-images.githubusercontent.com/33534771/75853699-f8468100-5e31-11ea-8c0f-5109f2852c59.png"/>

- LEFT OUTER JOIN의 반대이다.
- 오른쪽 테이블을 기준으로 Join을 하겠다고 생각하면 된다.
- 결과값은 B 테이블의 모든 데이터와 A 테이블과 B 테이블에서 중복되는 값이 검색된다.

```sql
SELECT
A.NAME,
B.AGE
FROM EX_TABLE A
RIGHT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```



**4) FULL OUTER JOIN**

<img src="https://user-images.githubusercontent.com/33534771/75853732-072d3380-5e32-11ea-8cda-53eb71de966e.png"/>

- 쉽게 말해 **합집합**을 생각하면 된다.
- A 테이블이 가지고 있는 데이터, B 테이블이 가지고 있는 **데이터 모두 검색된다.**
- 사실상, 기준 테이블의 의미가 없다.

```sql
SELECT
A.NAME,
B.AGE
FROM EX_TABLE A
FULL OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```


**5) CROSS JOIN**

<img src="https://user-images.githubusercontent.com/33534771/75853764-16ac7c80-5e32-11ea-9942-04adab33ddb2.png"/>

- **모든 경우의 수를 전부 표현해주는 방식**이다.
- 기준 테이블이 A일 경우, A의 데이터 한 ROW를 B 테이블 전체와 JOIN하는 방식이다.
- 결과값은 N*M이다.
- 위의 경우 A 테이블에 데이터가 3개, B 테이블에 데이터가 4개가 있으므로 총 12개가 검색된다.

```sql
--첫 번째 방식--
SELECT
A.NAME,
B.AGE
FROM EX_TABLE A
CROSS JOIN JOIN_TABLE B

--두 번째 방식--
SELECT
A.NAME,
B.AGE
FROM EX_TABLE A, JOIN_TABLE B
```



6) SELF JOIN

<img src="https://user-images.githubusercontent.com/33534771/75853799-2926b600-5e32-11ea-94ce-4974aade41ca.png"/>

- 자기 자신과 자기 자신을 조인한다는 의미이다.
- 하나의 테이블을 여러번 복사해서 조인한다고 생각하면 된다.
- 자신이 가지고 있는 칼럼을 다양하게 변형시켜 활용할 경우에 자주 사용한다.

```sql
SELECT
A.NAME,
B.AGE
FROM EX_TABLE A, EX_TABLE B
```



### 참고

[JOIN의 종류설명 및 사용법 & 예제](https://coding-factory.tistory.com/87)
