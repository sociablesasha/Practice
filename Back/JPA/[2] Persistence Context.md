# [2] Persistence Context

## 정의
* Persistence Context (영속성 컨텍스트).
* Server Side와 Database Side 사이에 엔티티를 저장하는 논리적인 영역.
## 특징
1. 1차 캐시
<br>영속성 컨텍스트에 엔티티 클래스를 저장하고 관리한다.

2. 동일성 보장
<br>캐시에 들어간 객체를 두번가져와서 비교하면 동일하다.

3. 변경 감지
<br>영속성 상태의 객체는 객체의 데이터가 변경이 되면, 자동 update 된다.
<br>EntityManager에서 flush가 되고, commit이 된다.

4. 트랜잭션으로 인한 쓰기 지연
<br>영속성 컨텍스트는 트랜잭션 범위 안에서 동작한다.

5. 지연로딩
<br>N + 1 쿼리라고 하는데, 엔티티와 관계가 맺어진 엔티티의 데이터를 가져 올 수 있다.


## JDBC 개발 VS JPA 개발 (내부적으로 JDBC 사용)
### JDBC 개발
쿼리를 실행하면 DB로 쿼리를 날린다.
### JPA 개발
아래와 같은 작업을 진행한다.
* 조회할 데이터가 영속성 컨텍스트에 존재하는지 확인한다.
* 데이터가 없으면 쿼리를 생성하고 DB에 전송한다.
* 결과값을 전달받고 엔티티로 저장한 후에 리턴한다.