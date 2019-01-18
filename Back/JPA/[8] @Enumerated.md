# [8] @Enumerated

## 정의
* 자바의 enum 타입을 엔티티 클래스의 속성으로 사용할 수 있다.

## Code
```java
@Entity
class EnumEntity {
    @Enumerated(EnumType.ORDINAL)
    // @Enumerated(EnumType.STRING)
    private Gender gender;

}

enum Gender {
    MALE,
    FEMALE;
}
```

## Attribute Converter VS @Enumerated
> @Enumerated를 사용하여 속성을 구현할 때, ORDINAL로 설정 후 Genber enum 타입이 변경된다면 예기치 못한 문제가 발생할 수 있기도 하고 STRING 설정은 문자열 자체가 저장되기 때문에 DB 공간 낭비가 발생한다.
> (탁구치는 개발자 https://lng1982.tistory.com/280)

위의 의견에 추가적인 설명을 덧붙이자면 Attribute Converter로 구현할 때에는 값과 변환할 값을 자유롭게 설정할 수 있지만 @Enumerated로 구현할 때에는 값만이 자유롭게 설정할 수 있기에 비추천한다. 
