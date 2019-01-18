# JPA-Before


## 정의
* ORM(Object Relational Mapping).
* RDB 테이블을 객체지향적으로 사용하기 위한 기술.
> ### xBatis VS JPA
> #### xBatis
> * 화면과 관련된 쿼리(XML파일) 생성.
> * 쿼리 결과 데이터를 저장하는 POJO 생성.
> * DAO (Data Access Object) 생성.
> * 추가, 삭제, 수정 등 변경에 대처가 어렵다.
> #### JPA
> * 테이블의 개수 = Entity의 개수 (DDD)
> * Entity 생성 및 객체 연관관계 설정.
> * 직접 작성해야하는 코드의 양 감소.


## Persistence Context (영속성 컨텍스트)
Server Side와 Database Side 사이에 엔티티를 저장하는 논리적인 영역.
> ### 장점
> 1. 1차 캐시
> <br>영속성 컨텍스트에 엔티티 클래스를 저장하고 관리한다.
> 2. 동일성 보장
> <br>캐시에 들어간 객체를 두번가져와서 비교하면 동일하다.
> 3. 변경 감지
> <br>영속성 상태의 객체는 객체의 데이터가 변경이 되면, 자동 update 된다.
> <br>EntityManager에서 flush가 되고, commit이 된다.
> 4. 트랜잭션으로 인한 쓰기 지연
> <br>영속성 컨텍스트는 트랜잭션 범위 안에서 동작한다.
> 5. 지연로딩
> <br>N + 1 쿼리라고 하는데, 엔티티와 관계가 맺어진 엔티티의 데이터를 가져 올 수 있다.


## EntityManagerFactory
EntityManager를 관리하기 위한 객체.


## EntityManager
Database Side에 엔티티를 반영하기 위한 객체.
> ### 생명주기
> 1. 비영속 (new)
> <br>일반적인 인스턴스이라고 볼 수 있다.
> 2. 영속 (managed)
> <br>EntityManager에 persist를 통해 인트스턴스를 영속성 컨텍스트에 넣어진 상태이다.
> 3. 준영속 (detached)
> <br>영속성 컨텍스트로부터 나온 객체이다.
> <br>detach, clear, close 등으로 가능하다.
> <br>식별자가 존재한다.
> <br>merge 로 다시 영속성 상태로 만들 수 있다.
> 4. 삭제 (removed)
> <br>Database Side에서 지워졌지만 영속성 컨텍스트에서는 존재하는 상태이다.
