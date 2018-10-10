# META Tag

## 정의
문서를 설명하는 요소이다. (제목, 키워드, 문자셋 등)

## 예시
```html
<!DOCTYPE html>
<html>
    <head>
        <!-- 문자셋(한글 깨짐 방지) -->
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />

        <!-- 검색엔진을 위한 키워드와 디스크립션 -->
        <meta name="Description" content="소개 내용" />
        <meta name="Keywords" content="키워드들의 나열, abc, 123" />

        <!-- 작성자 -->
        <meta name="author" content="your name" />

        <!-- 우회 및 새로고침 -->
        <meta http-equiv="refresh" content="10;url=http://google.com/" />

        <!-- IE 모드 -->
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />

        <!-- 뷰포트 -->
        <meta name="viewport" content="initial-scale=1.0" />
    </head>
    <body>
        ...
    </body>
</html>
```

## 결론
문서를 설명하는 요소인 메타 태그를 적절히 이용한다면 구글 또는 검색엔진을 사용하여 검색 시 우선 순위로 들 확률이 크며 한글이 깨지는 것을 방지하는 등 다양한 상황에 활용할 수 있다.