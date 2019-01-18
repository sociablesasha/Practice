# Closure

## 정의
내부함수가 외부함수의 지역변수에 접근 할 수 있고, 외부함수는 외부함수의 지역변수를 사용하는 내부함수가 소멸될 때까지 소멸되지 않는 특성을 의미한다.

## 함수
### 내부함수
```javascript
function outter () {
    function inner () {
        var title = "coding everyday!";
        return title;
    }
    inner();
}
outter();
```
위의 코드에서 함수 outter 내부에는 함수 inner가 정의 되어 있다. 함수 inner를 내부 함수라고 한다.

또한 아래의 코드와 같이 내부함수는 외부함수의 지역변수에 접근할 수 있다.
```javascript
function outter () {
    var title = "coding everyday!";
    function inner () {
        return title;
    }
    inner();
}
outter();
```

### 외부함수
위의 코드에서 함수 inner 내부에는 함수 outter가 정의 되어 있다. 함수 outter를 외부 함수라고 한다.


## 사용예시
```javascript
function factory_person (name) {
    return {
        get_name: function () {
            return name;
        },
        set_name: function (_name) {
            name = _name;
        }
    }
}
``` 
factory_person의 지역변수인 name을 접근하기 위해서는 오직 get_name()과 set_name() 밖에 존재하지 않는다. 이처럼 private variable를 구현할 수 있다.

## 오류
```javascript
var arr = []
for(var i = 0; i < 5; i++){
    arr[i] = function(){
        return i;
    }
}

for(var index in arr) {
    console.log(arr[index]());
}
```
위의 결과는 아마 0,1,2,3,4 같은 결과가 나올 것이라고 생각했다면 틀렸다.

아래와 같은 코드여야 생각하는 결과를 얻을 수 있을 것이다.
```javascript
var arr = []
for(var i = 0; i < 5; i++){
    arr[i] = function(id) {
        return function(){
            return id;
        }
    }(i);
}

for(var index in arr) {
    console.log(arr[index]());
}
```