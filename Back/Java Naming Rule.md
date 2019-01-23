# Java Naming Rule

## 패키지
- 하나의 단어만 사용할 것이 권장된다.
- 단어의 길이가 10자를 넘지 않는 것이 권장된다.
- 하위 패키지는 상위 패키지와 깊은 연관을 맺어야 한다.
### domain
단위로 표현할 수 있고 원자성을 띄는 자바빈 클래스, Enum 클래스 등이 위치한다.
### dao
데이터액세스 계층과 관련된 클래스와 인터페이스가 위치한다.
### service
dao를 조합하고 트랙잭션의 경계가 설정되는 구간이다.
### core
애플리케이션의 핵심적인 역할을 수행하는 클래스와 인터페이스가 위치한다.
### task
스레드와 관련된 java.lang.Runnable 클래스의 활동을 지원하는 클래스가 위치한다.
### access
리소스의 자원을 불러들이고 이를 자바에서 사용가능한 상태로 가공해주는 클래스가 위치한다.
### support
객체를 다른 클래스에서 요구하는 형태로 가공해주는 역할의 클래스와 부모 패키지의 인터페이스들이 구현된 클래스가 위치한다.
### config
다른 언어 또는 외부 자원을 자바의 형태로 파싱하고 그 설정을 구현체에 저장해준다.
### validation
부모 패키지의 객체들을 검증하는 검사자 클래스가 위치한다.
### util
부모 패키지의 객체들에 대한 작업을 도와주는 도구 클래스가 위치한다.



## 인터페이스
- 추상적이며 의미를 드러내야만 한다.
- 직관적이고 누구나 이해할 수 있는 단어로 선별한다.
- 전치사와 동사를 사용하지 않는 것이 좋다.



## 클래스
- Dependency Injection이 가능한 형태로 클래스를 만들어야 한다.
- 확장을 고려한다.
### Simple + 인터페이스명
인터페이스의 가장 기본적인 구현체를 구현한다.
### 용도명 + 인터페이스명
기본 구현체 외에 다른 방식을 이용된다면 용도를 접두어로 사용하는 클래스가 구현된다.
### 인터페이스명 + Utils
특정 구현체를 인자로 받아 다양한 역할을 수행해주는 도움 클래스를 지칭한다.



## 메소드
### get…
어떠한 리소스를 리턴하는 메서드
### set…
프로퍼티에 해당 리소스를 내장시키는 역할의 메서드 
### init…
초기값이 필요하다면 초기값을 설정하고 내부에서 관련 validate를 실행하는 역할의 메서드
### load…
전달인자를 기준으로 어떠한 값을 불러와 내장시켜주거나 카운팅하는 역할의 메서드
### is…
불리언 메서드에서 사용되는 접두어이다. 용도는 get…과 같다.
### has…
contains 메서드처럼 어떠한 값을 가지고 있는지 확인해준다. 다른 점이 있다면 contains는 좀 더 범위가 넓지만 has는 특정 값으로 범위가 한정되있다.
### register…
기본적으로 set과 동작하는 방식이 같지만 set은 자바빈 규약에 얽혀있기 때문에 복잡한 연산을 포함할 수 없다. 보다 지능적인 set이 요구될 때 register과 같은 접두어를 사용한다.
### create…
register…는 보통 void 형태이지만 create는 전달인자를 통해 새로운 객체를 만든 뒤에 이 객체를 리턴해준다.
### to…
많이 만들어두면 참 좋은 접두어 메서드이다. 해당 객체를 다른 형태의 객체로 변환해준다.
### A-By-B
B를 기준으로 A를 하겠다는 뜻
### A-With-B
B와 함께 A를 하겠다는 뜻
### …With
무엇과 함께 있는지, indexOf와 비슷한 성격의 접미사이다.
### …s
해당 객체가 복수의 객체를 반환하는지 단일 객체를 반환하는지 구분하는 것은 매우 중요하다. 복수형으로 표현해야 하는 메서드는 반드시 복수형으로 표현하여야 한다.