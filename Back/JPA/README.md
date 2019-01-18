# JPA


## 객체 그래프 탐색
RDB 테이블과 Entity 클래스가 1:1 매핑이 되는 구조이기에 화면(동작)이 추가된다고 하여서 Entity 클래스를 추가하지 않아도 된다. 객체 연관관계 설정을 잘하여 필요한 데이터가 있으면 객체를 타고 다니며 데이터를 사용할 수 있다.


## Hibernate, EclipseLink, ...
### JPA : 자바 ORM 기술에 대한 API 표준 명세를 의미한다.
결국 JPA는 ORM을 사용하기 위한 API이며, 그것을 구현한 Hibernate, EclipseLink 등 ORM Framework를 사용해야 한다.