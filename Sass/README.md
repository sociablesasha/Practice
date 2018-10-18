# Sass

## 정의
추가 기능과 유용한 도구를 제공하기 위해 CSS의 구문을 개선한 스타일시트 언어이다.

## SCSS
Sass의 3버전에서 새롭게 등장하였고 CSS 구문과 완전히 호환되도록 새로운 구문을 도입해 만들었다. (앞으로의 예제는 모두 SCSS로 작성된 것이다.)

## 변수
```SCSS
$primary-color: #3bbfce;
$margin: 16px;

.content-navigation {
  border-color: $primary-color;
  color: darken($primary-color, 10%);
}

.border {
  padding: $margin / 2;
  margin: $margin / 2;
  border-color: $primary-color;
}
```

## 네스팅
```SCSS
table.hl {
  margin: 2em 0;
  td.ln {
    text-align: right;
  }
}

li {
  font: {
    family: serif;
    weight: bold;
    size: 1.3em;
  }
}
```