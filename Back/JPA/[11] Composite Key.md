# [11] 복합키

## 정의
* 대부분의 엔티티에는 @Id 어노테이션을 한 개만 사용한다.
* 하지만 테이블의 키가 복합키로 이뤄져 있다면 엔티티를 설계할 때에 이를 고려해야 한다.


## @EmbeddedId VS @IdClass
> @Embeddable이 객체지향 방식에 가깝고, @IdClass은 DB 방식에 가깝다고 하는데 잘 와닿지는 않는다.
> (탁구치는 개발자 https://lng1982.tistory.com/280)

#### 아래의 코드를 구현하며 와닿은 것이다.
**@EmbeddedId** 이용한 개발은 복합키 객체들을 하나의 객체로서 관리할 수 있지만 직관성이 떨어진다. 하지만 변경 사항에 유연하게 대체하였다.

**@IdClass** 이용한 개발은 복합키 객체들을 하나의 객체로서 관리하며 엔티티에서 각각의 키들을 대조한다. 결국 하나의 객체에서 관리하는 키와 엔티티에서 각각의 복합키들을 대조하는 것이기에 직관성은 좋았지만 변경 사항이 생길 경우 2번의 일을 해야한다는 점이 귀찮았다. 



## Code (@EmbeddedId)
```java
@Embeddable
class EmpIdSerial implements Serializable {
    @Column(name = "EMP_NO")
    private int empNo;
 
    @Column(name = "EMP_NAME")
    private String empName;
}

@Entity
public class EmpId {
    @EmbeddedId EmpIdSerial id;
}
```

## Code (@IdClass)
```java
class EmpIdSerial implements Serializable {
    private int empNo;
    private int empName;
}

@Entity
@IdClass(EmpIdSerial.class)
class EmpId {
    @Id
    @Column(name = "EMP_NO")
    private int empNo;
 
    @Id
    @Column(name = "EMP_NAME") 
    private int empName;
}
```