# [16] N + 1 (@BatchSize)

## 정의
* 1번의 쿼리로 100개의 데이터를 가져와야 하는 경우
* N번의 추가 쿼리가 발생하는 문제


## 이유
1. cat 테이블 전체 조회 (200건 리턴)
2. cat 데이터 200건을 각각 영속화 진행
3. cat 엔티티의 owner 속성이 즉시 로딩으로 되어 있기에 owner 데이터를 가져오기 위한 쿼리


## Code
```java
@BatchSize(size = 10)
class Owner {
    @OneToMany(fetch = FetchType.EAGER, cascade = CascadeType.PERSIST, mappedBy = "owner")
    @BatchSize(size = 10)
    private List<Cat> cats = new ArrayList<>();
}

class Cat {
    @ManyToOne(fetch = FetchType.EAGER)
    private Owner owner;
}
```
