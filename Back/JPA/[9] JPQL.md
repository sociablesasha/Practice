# [9] JPQL

## 정의
* 테이블이 아닌 객체를 대상으로 검색하는 객체지향 쿼리이다.


## 특징
* JPQL을 실행하게 되면 영속성 컨텍스트가 flush 된다.
* JPQL로 조회한 엔티티는 영속 상태이다.


## 순서
1. JPQL 작성 후 실행하면 영속성 컨텍스트로 요청을 보낸다.
2. 영속성 컨텍스트는 1차 캐쉬에 엔티티 존재 여부 상관 없이 DB에 질의한다.
3. DB 질의를 통해 조회된 데이터는 영속성 컨텍스트가 받고 엔티티를 초기화한 후 캐쉬에 저장한다.
4. 캐쉬에 저장 후 엔티티를 반환한다.


## Code
```java
@Test
@Transactional
public void testJPQL() {
    em.createQuery("SELECT p FROM Person p")
        .getResultList()
        .forEach(System.out::println);
 
    Query query = em.createQuery("select p from Person p");
    List<Person> list = query.getResultList();
    assertThat(list.size(), is(CNT));
}
```