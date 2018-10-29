# 이벤트 바인딩 중복

## 정의
두 번 이상 이벤트를 바인딩을 함으로서 기존의 바인딩 된 이벤트와 중복으로 바인딩되게 된 상황을 말한다.

## 문제
```javascript
$(".bind").click(function () {
    alert('hi');
});

$(".bind").click(function () {
    console.log('hi');
});
```
위의 코드의 결과를 실행해본다면 감이 올 것이다. 하나의 웹 사이트를 개발해본 경험이 있다면 한 번쯤은 직면했을 상황이라고 확신한다.

위와 같은 상황일 때 너는 어떻게 해결한 것인가? 아래 두 가지의 해결법을 제시하겠다.

## 해결 - 이벤트 언바이딩
```javascript
$(".bind").click(function () {
    alert('hi');
});

$(".bind").unbind("click");

$(".bind").click(function () {
    console.log('hi');
});
```
이벤트를 언바이딩을 하는 것은 요소에 등록된 이벤트가 아닌 다른 이벤트로 바인딩하고 싶을 때 사용하자.

## 해결 - 이벤트 위임
```javascript
$(".binds").click(function (event) {
    console.log(event.target);
})
```
이벤트를 위임하는 것은 새롭게 추가되는 요소에 기존의 요소에 등록된 이벤트를 사용하고 싶을 때 사용하자.
