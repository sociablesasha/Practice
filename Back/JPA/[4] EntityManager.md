# [4] EntityManager

## 정의
* 특정 작업을 위해 데이터베이스에 액세스한다.
* 엔티티를 데이터베이스에 등록, 수정, 삭제, 조회를 할 수 있다.

## 특징
* 여러 쓰레드가 동시에 접근하면 동시성 문제가 발생하므로 쓰레드 간에는 무조건 공유하면 안 된다.

## @PersistenceContext
1. Spring 컨테이너가 초기화된다.
2. @PersistenceContext 어노테이션으로 주입받은 EntityManger를 Proxy로 감싼다.
3. 이후 EntityManager 호출 시 마다 Proxy를 통해 EntityManager를 생성하여 Thread-Safety를 보장한다.

## Code
```java
@PersistenceUnit
private EntityManagerFactory emf;
 
@PersistenceContext
private EntityManager em;
 
@Test
public void 엔티티매니저_호출시마다_새로운인스턴스리턴() {
    EntityManager em1 = emf.createEntityManager();
    EntityManager em2 = emf.createEntityManager();
    EntityManager em3 = emf.createEntityManager();
 
    System.out.println(em1);
    System.out.println(em2);
    System.out.println(em3);
    System.out.println(em);
 
    assertThat(em1, is(not(sameInstance(em2))));
    assertThat(em1, is(not(sameInstance(em3))));
    assertThat(em, is(not(sameInstance(em1))));
    assertThat(em, is(not(sameInstance(em2))));
    assertThat(em, is(not(sameInstance(em3))));
}
```