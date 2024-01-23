## CASE
조건에 따라서 값을 지정
```sql
CASE 컬럼
	WHEN 조건1 THEN 값1
	WHEN 조건2 THEN 값2
	ELSE 값3
END
```

https://121202.tistory.com/46
## COALESCE
https://leetcode.com/problems/find-customer-referee/solutions/2398637/simple-query-with-easy-null-handling-using-coalesce/?envType=study-plan-v2&envId=top-sql-50

## UNION
or 대신에 쓸 수 있는 절?
or보다 UNION이 더 빠를 때도 있다고 함
https://leetcode.com/problems/big-countries/solutions/103561/union-and-or-and-the-explanation/?envType=study-plan-v2&envId=top-sql-50

DISTINCT
중복된 데이터를 제거하고 데이터 취득

https://www.javadrive.jp/mysql/select/index13.html

## JOIN

두 테이블에 모두 내용이 있을 때 이너조인
한쪽에만 내용이 있거나 불완전? 할 때 외부조인
### INNER JOIN
조인된 두 테이블에서, 조인 기준이 된 칼럼에 데이터가 양쪽 모두 존재하는 경우에만 결과값 출력
보통 조인이라고 하면 이너조인임 
### OUTER JOIN
기준이 되는 테이블의 모든 레코드를 출력함 LEFT / RIGHT / FULL
FULL은 잘 사용안됨
LEFT JOIN 
https://makand.tistory.com/entry/SQL-LEFT-JOIN-%EA%B5%AC%EB%AC%B8

### on 과 where 차이
on : join 전에 조건을 필터링
where : Join 후에 조건을 필터링
https://velog.io/@crosstar1228/SQL-join%ED%95%A0%EB%95%8C-on-%EA%B3%BC-where%EC%9D%98-%EC%B0%A8%EC%9D%B4

## GROUP BY

## DATEDIFF

https://mirwebma.tistory.com/178

## 논리 연산자

## 비교 연산자
<> : !=랑 같음. 두 값이 다르면 TRUE