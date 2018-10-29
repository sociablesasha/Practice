# Prototype

## 정의
자바를 공부한 사람은 객체지향 언어를 떠올리면 제일 먼저 클래스가 생각날 것이다. 하지만 객체지향을 표현하는 방법은 무수히 많고 클래스는 그 중 하나고 프로토타입은 또 다른 하나다.

## 클래스와 프로토타입의 차이점
### 클래스 기반 언어
1. 객체의 형식이 정의된 **클래스**라는 개념을 갖는다.
2. 또한 클래스 기반 언어만의 상속이라는 개념을 갖는다.

자바에서 클래스를 하나의 객체로 본다. 그렇다면 '클래스가 참조한 클래스는 누구이며 참조한 클래스가 참조한 클래스는 또 누구일까?'라는 물음에 닿고 이 문제를 우리는 'inifnite regress problem of classes'라고 말한다.

### 프로토타입 기반 언어
1. 클래스라는 개념이 존재하지 않으며, 여러 종류의 Built-in 객체들이 존재한다.
2. 상속 개념과 달리 위임이라는 개념을 갖는다.

즉 자바스크립트의 함수는 생성자 함수 객체 원형을 참조하는 또 다른 함수 객체일뿐이다.

## 예시
```javascript
function Person(name) {
    this.name = name;
}
        
Person.prototype.eyes = 2;
Person.prototype.nose = 1;

var kim = new Person("kim");
var park = new Person("park");

console.log(kim.eyes);
console.log(park.nose);
```

## 흐름
1. 함수가 정의된다.
2. 해당 함수에 constructor 부여한다.
3. 해당 함수의 Prototype Object 생성 및 연결한다.

## 참조
https://medium.com/@bluesh55/javascript-prototype-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-f8e67c286b67