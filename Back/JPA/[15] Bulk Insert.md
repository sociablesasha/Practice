# [15] Bulk Insert

## 정의
* 한 번에 대량의 데이터를 저장해야만 경우.
* 특정 개수로 나눠 영속화와 Flush를 반복.


## Code
```java
public class BulkTest {
 
    @PersistenceContext
    private EntityManager em;
 
    @Value("${spring.jpa.properties.hibernate.jdbc.batch_size}")
    private int batchSize;

     @Test
    @Transactional
    public void bulkInsert() {
        for (int i = 0; i < 10000; i++) {
            BulkMember member = new BulkMember();
            member.setId(i);
            member.setName("nklee");
            em.persist(member);
 
            if (i % batchSize == 0) {
                em.flush();
                em.clear();
            }
        }
 
        em.flush();
        em.clear();
    }
}
```


## 예외
### @GeneratedValue(strategy = GenerationType.IDENTITY)
1. DB 저장한다.
2. auto_increment 생성된 값을 가져온다.
3. 엔티티를 영속화한다.
