# WeakMap

## 정의
WeakMap은 오브젝트만을 키로 허용하고 임의의 값을 허용한다. WeakSet도 오브젝트만을 요소로 허용한다. 또한, 객체에 대한 참조가 더이상 존재하지 않을경우 가비지 컬렉션의 대상이 된다. 즉, 언제든지 오브젝트가 GC의 대상이 될수 있기 때문에 WeakMap은 키들의 열거형을 지원하지 않는다.

## GC와의 연관성
key로 사용하고 있던 Object 오브젝트가 메모리에서 사라질 경우, 즉 GC에 의해서 Garbage Colleting이 되면, 더이상 value의 key로서 역할을 수행하지 못한다. 그렇기 때문에 이 key에 대한 내용을 삭제해줘야 한다. 메모리에서 사라진 key에 대해서 삭제하는 작업을 WeakMap을 사용하면 자동으로 해결된다.

## 예제
```javascript
let exWeakMap = new WeakMap();

let object = { "item": "hohohohoho" };

exWeakMap.set(object, "GC");
```