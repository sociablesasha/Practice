# Promise


## 정의
프로미스는 자바스크립트 비동기 처리에 사용되는 오브젝트이다. 여기서 자바스크립트의 비동기 처리란 ‘특정 코드의 실행이 완료될 때까지 기다리지 않고 다음 코드를 먼저 수행하는 자바스크립트의 특성’을 의미한다.


## 예제
### 적용 전
```javascript
function getData(callbackFunc) {
    $.get('url 주소/products/1', function (response) {
        callbackFunc(response);
    });
}

getData(function (tableData) {
    console.log(tableData);
});
```
### 적용 후
```javascript
function getData(callback) {
    return new Promise(function (resolve, reject) {
        $.get('url 주소/products/1', function (response) {
            resolve(response);
        });
    });
}

getData().then(function (tableData) {
    console.log(tableData);
});
```


## 상태
### 대기
```javascript
new Promise(function (resolve, reject) {
  // ...
});
```
### 이행
```javascript
new Promise(function (resolve, reject) {
    // Fulfilled
    resolve();
});
```
### 실패
```javascript
new Promise(function (resolve, reject) {
    // Rejected
    reject();
});
```