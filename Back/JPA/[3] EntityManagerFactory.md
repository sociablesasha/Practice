# [3] EntityManagerFactory

## 정의
* 엔티티 매니저 팩토리는 엔티티 매니저를 관리한다.
* 애플리케이션 전체에서 딱 한 번만 생성하고 공유해서 사용해야 한다.
* 엔티티 매니저 팩토리는 여러 쓰레드가 동시에 접근할 수 있다.

## Code
```java
@PersistenceUnit
private EntityManagerFactory emf;
 
@Resource(name = "entityManagerFactoryTest")
private EntityManagerFactoryTest entityManagerFactoryTest;
 
@Test
public void 엔티티매니저팩토리_인스턴스_체크() {
    assertThat(emf, is(sameInstance(entityManagerFactoryTest.getEmf())));                                   // True
    assertThat(emf, is(sameInstance(entityManagerFactoryTest.getEmf2())));                                  // True
    assertThat(entityManagerFactoryTest.getEmf(), is(sameInstance(entityManagerFactoryTest.getEmf2())));    // True
}
    
@Service("entityManagerFactoryTest")
class EntityManagerFactoryTest {
    @Getter
    @PersistenceUnit
    private EntityManagerFactory emf;
    
    @Getter
    @PersistenceUnit
    private EntityManagerFactory emf2;
}
```