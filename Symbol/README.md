# Symbol

## 정의
ES6에서 새롭게 추가된 래퍼 객체이다.

## 탄생 배경
ES5에서 Array인지 아닌지 구분하는 표준화된 방법이 없다. typeof 연산자를 써도 object를 반환하기 때문에 구분해낼 방법이 없다. 따라서 아래와 같이 함수화시켜서 라이브러리로 제작 후에 많은 사람에게 배포했다고 가정하자.
```javascript
Array.isArray = function(arg) {
  return (Object.prototype.toString.call(arg) === '[object Array]') ? 'true-String' : 'false-String';
};
```
하지만 ES6 들어서 위에 우리가 사용한 Array.isArray 메소드가 표준 메소드로 지정되었기에 그 메소드는 우리가 예측한 문자열들이 아닌 Boolean 값을 반환하는 메소드다. 따라서 우리 라이브러리를 사용해서 개발한 사용자들의 코드가 의도한 대로 작동하지 않을 가능성이 있다. 하지만 다행히도 위 메소드는 덮어쓰기가 가능하다. 그래도 우리 라이브러리를 쓰는 개발자가 ES6의 표준 메소드 작동 방식으로 Array.isArray를 썼다간 낭패를 볼 것이다. 위에서 봤 듯이 표준 객체에 혹시 내가 쓴 프로퍼티가 표준 프로퍼티가 되는 불상사가 생긴다면 코드가 의도치 않게 작동할 것이다.