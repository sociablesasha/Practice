# Class

## 정의
클래스(class)는 객체 지향 프로그래밍(OOP)에서 특정 객체를 생성하기 위해 변수와 메소드를 정의하는 일종의 틀이다.

## 자바스크립트는 프로토타입이 아니였나?
ES6의 클래스는 기존 프로토타입 기반 객체지향 프로그래밍보다 클래스 기반 언어에 익숙한 프로그래머가 보다 빠르게 학습할 수 있는 단순명료한 새로운 문법을 제시하고 있다. 그렇다고 ES6의 클래스가 새로운 객체지향 모델을 제공하는 것은 아니며, 사실 클래스도 함수이고 기존 프로토타입 기반 패턴의 Syntactic sugar일 뿐이다.

## 선언
```javascript
class Member {
// ...
};
```

## 생성
```javascript
class Member {
// ...
};

let object = new Member();
```

## 초기화
```javascript
class Member {
    constructor(name) {
        this.name = name;
    }
};

let object = new Member("Kim");
```

## setter, getter
```javascript
class Member {
    constructor(name) {
        this.name = name;
    }
    set setName(name) {
        this.name = name;
    }
    get getName() {
        return name;
    }
};

let object = new Member("Kim");
```

## 상속
```javascript
class Member {
    constructor(name) {
        this.name = name;
    }
    set setName(name) {
        this.name = name;
    }
    get getName() {
        return name;
    }
};

class ClassMate extends Member {
    constructor(grade) {
        this.grade = grade;
    }
    set setGrade(grade) {
        this.grade = grade;
    }
    get getGrade() {
        return grade;
    }
};

let object = new ClassMate("Kim");
```