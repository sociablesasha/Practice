# Conditional Compile (조건부 컴파일)

## 정의
조건부 컴파일을 사용하면 새로운 JavaScript 언어 기능을 지원하지 않는 이전 버전과 호환성을 유지하면서 새 언어 기능을 사용할 수 있다.

## 예시
```javascript
/*@cc_on @*/
/*@if (@_jscript_version >= 4)
    alert("JavaScript version 4 or better");
    @else @*/
    alert("Conditional compilation not supported by this scripting engine.");
/*@end @*/
```
만약 브라우저 버전이 4 이상이라면 주석으로 해놓은 코드가 실행이 되면서 "JavaScript version 4 or better"이라는 문구가 나올 것이고 아니라면 주석을 실행하지 않은 "Conditional compilation not supported by this scripting engine."라는 문구가 나올 것이다.