# var vs let,const

## var(function-scoped)
```javascript
for(var i=0; i<10; i++) {}
console.log('after loop i is ', i);
```

위의 결과를 예상해보자. 기존의 C언어나, Java를 알고 있다면 출력문이 에러가 나야만 할 것이다. 하지만 자바스크립트에서의 변수와 함수 선언은 호이스팅 되기에 'after loop i is 10'이라는 값이 나올 것이다.

```javascript
function counter () {
  for(var i=0; i<10; i++) {}
}
counter()
console.log('after loop i is', i)
```

위의 경우 var가 function-scoped이기에 i를 찾지 못하고 'ReferenceError: i is not defined'이라는 값이 나온다. 그렇다면 항상 함수를 만들어야만 할까? 아니다. 자바스크립트에는 IIFE를 지원하기에 function-scoped인 거 처럼 만들 수 있다.

```javascript
(function() {
  for(var i=0; i<10; i++) {
    console.log('i', i)
  }
})()
console.log('after loop i is', i)
```

결과는 'ReferenceError: i is not defined'이라는 값이 나온다. 하지만 아래의 경우 변수 i가 Global Variable로 호이스팅되기에 다시 결과는 'after loop i is 10'이라는 값이 나온다.

```javascript
(function() {
  for(i=0; i<10; i++) {
    console.log('i', i)
  }
})()
console.log('after loop i is', i)
```

그렇다면 var의 특성과 hoist로 인해 상황마다 바뀔 수 있는 코드를 신뢰해야할까?

## let,const(block-scoped)
var와의 가장 큰 차이점은 같은 스코프 내의 변수의 재선언이 허용되지 않는다.
```javascript
var a = 10;
var a = 20;
// 에러가 발생하지 않는다.

let a = 10;
let a = 20;
// 에러가 발생한다.
```

또한 let, const조차 호이스팅 된다. 하지만 스코프 자체가 block이기에 훨씬 안정적으로 코딩할 수 있다.
```javascript
for (let i = 0; i < 10; i++) {}
console.log(i);
//에러가 발생한다.
```
