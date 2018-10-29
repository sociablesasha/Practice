# Delegation

## 정의
이벤트 버블링과 캡쳐를 이용하여 하위의 이벤트를 각각 관리하는 것이 아닌 상위 요소의 이벤트로서 하위 요소의 이벤트를 제어하는 것이다.

## 이벤트 위임이 없었다면
```html
<h1>오늘의 할 일</h1>
<ul class="itemList">
	<li>
		<input type="checkbox" id="item1">
		<label for="item1">이벤트 버블링 학습</label>
	</li>
	<li>
		<input type="checkbox" id="item2">
		<label for="item2">이벤트 캡쳐 학습</label>
	</li>
</ul>

<script>
var inputs = document.querySelectorAll('input');
inputs.forEach(function(input) {
	input.addEventListener('click', function(event) {
		alert('clicked');
	});
});
</script>
```
1. 새롭게 추가되는 리스트와 카드들의 이벤트를 일일히 달아주었다.
2. 코드가 더러워졌다.
3. 깔끔하게 하기 위해 새롭게 추가할 때, 관련된 모든 클래스의 이벤트를 한 번에 달아주는 함수를 사용했다.
4. 중복으로 이벤트가 바인딩됨으로서 이벤트가 중복으로 발생했다.
4. 이를 해결하기 위해 함수 맨 윗 줄에 이벤트를 언바이딩해주는 코드를 추가했다.

트렐로를 제작한 경험이 있는 난 위와 같은 문제를 직면했고 해결했다. 하지만 이렇게 해결하지 않아도 이벤트 위임을 통해서 구현했었다면 위와 같은 문제또한 없었을 것이다. (지금은 수정한 상태이다.)

이렇듯 하위의 요소에 각각 이벤트 리스너를 추가하고 이벤트를 관리하는 것 또한 하나의 방법이지만 많아지면 많아질수록 이벤트 리스너를 다는 작업 자체가 매우 번거롭다. 따라서 난 하위의 요소가 늘어나며 이벤트 또한 달아줘야 한다면 이벤트 위임을 사용하는 것이 더 현명하다고 생각한다.


## 이벤트 위임을 사용하면
```html
<h1>오늘의 할 일</h1>
<ul class="itemList">
	<li>
		<input type="checkbox" id="item1">
		<label for="item1">이벤트 버블링 학습</label>
	</li>
	<li>
		<input type="checkbox" id="item2">
		<label for="item2">이벤트 캡쳐 학습</label>
	</li>
</ul>

<script>
var itemList = document.querySelector('.itemList');
itemList.addEventListener('click', function(event) {
	alert('clicked');
});
</script>
```
더 간편하고 가독성이 좋은 코드가 된 것을 확인할 수 있다.