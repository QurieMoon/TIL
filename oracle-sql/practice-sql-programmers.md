# Oracle SQL 연습
 - 프로그래머스 Oracle 예제를 풀면서 습득한 팁 정리하는 페이지

## WHERE절
 - Column "CREATED_DATE"의 data type이 DATE
 - 2022년 10월을 기준으로 필터링하고 싶다면?
``` sql
WHERE TO_CHAR(CREATED_DATE, 'YYYYYMMDD') LIKE '202210%'

```