# [19] lombok

## 정의
자바에서 Model Object를 만들때, 멤버필드에 대한 Getter/Setter, ToString과 멤버필드에 주입하는 생성자를 만드는 코드 등 불필요하게 반복적으로 만드는 코드를 어노테이션을 통해 줄여 주는 라이브러리, 프로젝트이다.
- gettter, setter
- toString
- builder
- etc...


## Annotation
### @Getter
Getter 메소드를 생성한다.

### @Setter
Setter 메소드를 생성한다.

### @ToString
toString 메소드를 클래스 필드를 확인해서 적절히 만든다.

### @EqualsAndHashCode
equals와 hashcode 메소드를 생성한다.

### @NonNull
Null을 허용하지 않는다.

### @Cleanup
Local Variable이 현재 code가 종료될 때 자동으로 호출된다.
> 1. close() 있으면 자동으로 호출한다.
> 2. 다른 method가 cleanup을 수행한다.

### @Data
- @ToString
- @EqaulsAndHashCode
- @Getter
- @Setter
- RequiredArgsConstructor

### @Value
필드를 변경할 수 없는 @Data를 생성한다.


### @Accessors
method chaining을 허용한다.


### @NoArgsConstructor, @AllArgsConstructor, @RequiredArgsConstructor
클래스의 생성자를 만들어준다.
