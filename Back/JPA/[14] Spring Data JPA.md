# [14] Spring Data JPA

## 정의
* Spring Data 프로젝트 하위에 존재.
* JPA를 쉽게 사용할 수 있도록 제공해주는 프로젝트.


## JpaRepository
* 미리 정해진 룰에 따라 메소드 이름을 붙인다.


## Code
```java
@Repository
public interface SampleEntityRepository extends JpaRepository<SampleEntity, Long> {
    public List<SampleEntity> findByNameLike(String name);
    public List<SampleEntity> findByMailEndingWith(String mail);
}
```