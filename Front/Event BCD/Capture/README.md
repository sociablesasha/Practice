# Capture

## 정의
이벤트 버블링과 반대 방향으로 진행되는 이벤트 전파 방식이다.

## 예시
```html
<div class="one">
	<div class="two">
		<div class="three">
		</div>
	</div>
</div>

<script>
var divs = document.querySelectorAll('div');
divs.forEach(function(div) {
	div.addEventListener('click', logEvent, {
		capture: true
	});
});

function logEvent(event) {
	console.log(event.currentTarget.className);
}
</script>
```
여기서 최하위 태그인 ```<div class="three"></div>```를 클릭하면 아래와 같이 결과값이 나온다.
```
one
two
three
```
