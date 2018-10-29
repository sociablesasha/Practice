# Bubble

## 정의
특정 요소에서 이벤트가 발생했을 때 해당 이벤트가 상위의 요소들로 전달되는 방식을 말한다.

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
	div.addEventListener('click', logEvent);
});

function logEvent(event) {
	console.log(event.currentTarget.className);
}
</script>
```
여기서 최하위 태그인 ```<div class="three"></div>```를 클릭하면 아래와 같이 결과값이 나온다.
```
three
two
one
```
