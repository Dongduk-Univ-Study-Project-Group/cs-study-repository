- 하나의 테이블에 원하는 데이터가 모두 있다면 좋지만, 두 개의 테이블을 엮어야 원하는 결과가 나오는 경우도 많다.
- 이때, JOIN을 사용하면 두 개의 테이블을 엮어 원하는 데이터를 추출할 수 있다.
- 두 테이블의 조인을 위해서는 기본키와 외래키 관계로 맺어져야 하고, 이를 **일대다 관계**라고 한다.
- 연결하기 위해서는 테이블들이 적어도 하나의 컬럼을 공유해야한다.

## JOIN

![스크린샷 2023-01-22 오후 9.35.39.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c9c3a298-2063-4cf2-8080-e3c62b965afe/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2023-01-22_%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE_9.35.39.png)

- 조인은 **두 개의 테이블을 서로 묶어서 하나의 결과**를 만들어 내는 것을 말한다.
- INNER JOIN(내부 조인): 두 테이블을 조인할 때, 두 테이블에 모두 지정한 열의 데이터가 있어야 한다. - 교집합
- OUTER JOIN(외부 조인): 두 테이블을 조인할 때, 1개의 테이블에만 데이터가 있어도 결과가 나온다. - 합집합
    - 오라클은 OUTER JOIN이 있지만, MYSQL은 없기 때문에 LEFT + RIGHT 조인 - 부분집합
- CROSS JOIN(상호 조인): 한쪽 테이블의 모든 행과 다른 쪽 테이블의 모든 행을 조인하는 기능이다.
- SELF JOIN(자체 조인): 자신과 자신이 조인한다는 의미로 1개의 테이블을 사용한다.

## INNER JOIN

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/40508b43-93b1-4e33-93e5-df6bcc48e920/Untitled.png)

```sql
SELECT <열 목록>
FROM <첫 번째 테이블>
      INNER JOIN <두 번째 테이블>
      ON <조인될 조건>
[WHERE 검색 조건]

* INNER JOIN을 JOIN이라고만 써도 INNER JOIN으로 인식합니다.
```

- 두 테이블을 연결할 때 가장 많이 사용하는 것
- 일반적으로 조인은 내부 조인을 의미한다.
- 교차 결합에 WHERE 조건을 추가하여 조건에 맞는 데이터들만 조회하는 방식
- ON 절과 함께 사용되며, ON 절의 조건을 만족하는 데이터만 가져온다.
    - ON 절에서는 WHERE 절에서 사용할 수 있는 모든 조건을 사용할 수 있다.
- 표준 SQL과 달리 MySQL에서는 JOIN, INNER JOIN, CROSS JOIN이 모두 같은 의미로 사용된다.
- 특정 컬럼이 같은 데이터를 조회하도록 조건을 추가시킨 결합을 동등 결합이라고 한다.

## OUTER JOIN

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6ade5ffd-c2df-4d68-8ac3-b0fe3cef537f/Untitled.png)

```sql
SELECT <열 목록>
FROM <첫 번째 테이블(LEFT 테이블)>
      <LEFT | RIGHT | FULL> OUTER JOIN <두 번째 테이블(RIGHT 테이블)>
       ON <조인될 조건>
[WHERE 검색 조건]
```

- 내부 조인은 두 테이블에 모두 데이터가 있어야만 결과가 나오지만, **외부 조인은 한쪽에만 데이터가 있어도 결과가 나온다.**

### 종류

1. LEFT OUTER JOIN: **왼쪽 테이블의 모든 값**이 출력되는 조인
2. RIGHT OUTER JOIN: **오른쪽 테이블의 모든 값**이 출력되는 조인
3. FULL OUTER JOIN: **왼쪽 또는 오른쪽 테이블의 모든 값이 출력**되는 조인

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dacb9793-ec84-4375-91eb-6ddf5a916dd7/Untitled.png)

## CROSS JOIN

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b5c1fe54-40bc-434c-b9fe-cfa228c2b52f/Untitled.png)

```sql
SELECT * 
FROM <첫 번째 테이블>
         CROSS JOIN <두 번째 테이블>
```

- 한쪽 테이블의 모든 행과 다른 쪽 테이블의 모든 행을 조인시키는 기능이다.
- 상호 조인 결과의 전체 행 개수는 두 테이블의 각 행의 개수를 곱한 수만큼 된다.
- 카티션 곱(CARTESIAN PRODUCT) 이라고도 한다.

## SELF JOIN

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7736b388-bddb-406e-bea3-760f7e0d420a/Untitled.png)

```sql
SELECT <열 목록>
FROM <테이블> 별칭A
        INNER JOIN <테이블> 별칭B
        ON <조인될 조건>
[WHERE 검색 조건]
```

- 자체 조인은 자기 자신과 조인하므로 한 개의 테이블을 사용한다.
- 별도의 문법이 있는 것은 아니고 1개로 조인하면 자체 조인이 된다.

## LEFT JOIN

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/30514ba3-57f6-4978-b01c-179f68170836/Untitled.png)

- 첫번째 테이블을 기준으로 두번째 테이블을 조합한다.
- ON 절의 조건을 만족하지 않는 경우, 첫번째 테이블의 필드 값은 그대로 가져오지만, 해당 레코드의 두번째 테이블의 필드 값은 모두 NULL로 표시된다.

## RIGHT JOIN

- LEFT 조인과는 반대로 두번째 테이블을 기준으로 첫번째 테이블을 조합하는 JOIN
- ON 절의 조건을 만족하지 않는 경우에는 두번째 테이블의 필드 값은 그대로 가져오지만, 해당 레코드의 첫번째 테이블의 필드 값은 모두 NULL로 표시된다.

## 참고 자료

- [https://hongong.hanbit.co.kr/sql-기본-문법-joininner-outer-cross-self-join/](https://hongong.hanbit.co.kr/sql-%EA%B8%B0%EB%B3%B8-%EB%AC%B8%EB%B2%95-joininner-outer-cross-self-join/)
- [https://pearlluck.tistory.com/46](https://pearlluck.tistory.com/46)
- [http://www.tcpschool.com/mysql/mysql_multipleTable_join](http://www.tcpschool.com/mysql/mysql_multipleTable_join)
- [https://victorydntmd.tistory.com/141](https://victorydntmd.tistory.com/141)