# Ajax

## 정의
Ajax는 **비동기**적인 웹 애플리케이션 제작을 위해 아래와 같은 조합을 이용하는 웹 개발 기법이다.
* 표현 정보를 위한 HTML, CSS
* 동적인 화면 출력 및 표시 정보와의 상호작용을 위한 DOM, 자바스크립트

## 기존의 웹
기존의 웹 애플리케이션은 브라우저에서 폼을 채우고 이를 웹 서버로 제출을 하면 하나의 요청으로 웹 서버는 요청된 내용에 따라 처리를 한후 새로운 페이지를 작성하고 응답으로 되돌려준다. 서버의 응답을 기다려야 하기에 사용자와 대화하는 애플리케이션의 개발이 어려웠다.

하지만 Ajax 애플리케이션은 필요한 데이터만을 요청해서 받은 후 클라이언트에서 처리할 수 있다. 또한 서버의 응답을 기다리는 동안 다른 작업을 할 수 있어 매우 효율적이다.

## XMLHttpRequest
```javascript
var xhr = new XMLHttpRequest();
xhr.onreadystatechange = function() {
    if (xhr.readyState === xhr.DONE) {
        if (xhr.status === 200) {
            console.log(xhr.responseText);
        } else {
            console.log(xhr.responseText);
        }
    }
};

xhr.open('GET', 'http://localhost');
xhr.send();
```
위의 예제는 대부분의 플러그인, 라이브러리의 기초가 되는 XMLHttpRequest 객체를 직접 이용하여 비동기 처리를 하는 코드이다. 나 또한 하나의 웹 프로젝트에서 모든 비동기 요청을 이 객체를 만들어 사용한 적도 있다. 하지만 더 간단하게 할 수 있는 방법이 있기에 소개하려 한다.

## jQuery.Ajax()
```javascript
$.ajax({
    url:'http://localhost',
    success:function(data) {
        console.log(data);
    },
    error:function(error) {
        console.log(error);
    }
});
```
한 눈에 보기 편해졌지 않은가? 위의 코드로 클라이언트는 서버와 비동기처리를 할 수 있다.