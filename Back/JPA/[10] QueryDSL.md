# [10] QueryDSL

## 정의
* 오픈 소스 프로젝트이다.
* type-safe한 쿼리를 위한 Domain Specific Language이다.


## 특징
* QueryDSL -> JSQL -> SQL



## 순서
1. JPQL 작성 후 실행하면 영속성 컨텍스트로 요청을 보낸다.
2. 영속성 컨텍스트는 1차 캐쉬에 엔티티 존재 여부 상관 없이 DB에 질의한다.
3. DB 질의를 통해 조회된 데이터는 영속성 컨텍스트가 받고 엔티티를 초기화한 후 캐쉬에 저장한다.
4. 캐쉬에 저장 후 엔티티를 반환한다.


## Code
```java
// QueryDslRepositorySupport 확장하여 사용한다.
@Test
@Transactional
public void Where조건() {
    QDslMember member = QDslMember.dslMember;
 
    JPQLQuery jpqlQuery = from(member);
    jpqlQuery.where(member.name.eq("nklee"));
    List<DslMember> result = jpqlQuery.fetch();
    assertThat(1, is(result.size()));
}
```