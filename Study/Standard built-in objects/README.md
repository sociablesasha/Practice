# 표준 내장 객체

## 정의
자바스크립트가 기본적으로 가지고 있는 객체들을 의미한다.
* Object
* Function
* Array
* String
* Boolean
* Number
* Math
* Date
* RegExp

## 확장
```javascript
var arr = new Array('seoul','new york','ladarkh','pusan', 'Tsukuba');
function getRandomValueFromArray(haystack){
    var index = Math.floor(haystack.length*Math.random());
    return haystack[index]; 
}
console.log(getRandomValueFromArray(arr));
```
위의 코드를 표준 내장 객체의 확장을 통해 구현하겠다.
```javascript
Array.prototype.rand = function(){
    var index = Math.floor(this.length*Math.random());
    return this[index];
}
var arr = new Array('seoul','new york','ladarkh','pusan', 'Tsukuba');
console.log(arr.rand());
```
