# [12] Transaction Isolation Level

## 정의
* Transaction Isolation Level (트랜잭션 격리 수준)
* 격리성은 동시에 실행된 트랜잭션이 서로에게 영향을 미치지 않도록 격리한다.


## 수준
1. READ UNCOMMITTED (커밋되지 않는 읽기)
2. READ COMMITED (커밋된 읽기)
3. REPEATABLE READ (반복 가능한 읽기)
4. SERIALIZABLE (직렬화 기능)


## READ UNCOMMITTED (커밋되지 않는 읽기)
트랜잭션 A가 특정 컬럼 데이터를 변경하고 있는 중에(커밋하지 않은 상태) 트랜잭션 B가 read하면 트랜잭션 A가 변경한 데이터를 읽어온다.

## READ COMMITTED (커밋된 읽기)
트랜잭션 A가 특정 컬럼 데이터를 변경하고 있는 중에(커밋하지 않은 상태) 트랜잭션 B가 read하면 트랜잭션 A가 변경하기 전 데이터를 읽어온다. 만약 트랜잭션 A가 데이터 변경 후 커밋하게 되면 트랜잭션 B는 변경된 데이터를 읽어온다.

## REPEATABLE READ (반복 가능한 읽기)
다른 트랜잭션에서 데이터를 조작하여도 영향을 받지 않는다.

## SERIALIZABLE (직렬화 기능)
트랜잭션이 완료될 때까지 SELECT 문장이 사용하는 모든 데이터에 Shared Lock이 걸리므로 다른 사용자는 그 영역에 해당되는 데이터에 수정 및 입력이 불가능하다.

## DB TIL
* MSSQL : READ COMMITTED
* MYSQL : REPEATABLE READ
* ORACLE : READ COMMITTED
* H2 : READ COMMITTED