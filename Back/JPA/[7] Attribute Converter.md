# [7] Attribute Converter

## 정의
* 개발을 진행하면 DB에는 코드성의 데이터가 쌓이게 된다. (1: ?, 2: ?, 3: ?)
* 코드성의 데이터를 화면에 출력하는 일은 거의 없다.
* 개발자의 편의성과 코드 관리의 어려움을 해소하고자 변환기가 구현되었다.

## Code
```java
@Entity
class ConverterEntity {
    @Convert(converter = ConverterTest.class)
    private int gender;
}
 
@Converter
public class ConverterTest implements AttributeConverter<String, Integer> {
    @Override
    public Integer convertToDatabaseColumn(String s) {
        if ("남자".equals(s)) {
            return 1;
        } else if ("여자".equals(s)) {
            return 2;
        }
        return 0;
    }
 
    @Override
    public String convertToEntityAttribute(Integer code) {
        if (1 == code) {
            return "남자";
        } else if (2 == code) {
            return "여자";
        }
        return "뭐지?";
    }
}
```