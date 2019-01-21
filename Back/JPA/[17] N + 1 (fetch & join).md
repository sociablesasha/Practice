# [17] N + 1 (fetch & join)

## 정의
* 1번의 쿼리로 100개의 데이터를 가져와야 하는 경우
* N번의 추가 쿼리가 발생하는 문제


## 이유
1. cat 테이블 전체 조회 (200건 리턴)
2. cat 데이터 200건을 각각 영속화 진행
3. cat 엔티티의 owner 속성이 즉시 로딩으로 되어 있기에 owner 데이터를 가져오기 위한 쿼리


## Code
### pom.xml
```xml
<dependency>
    <groupId>com.querydsl</groupId>
    <artifactId>querydsl-core</artifactId>
</dependency>

<dependency>
    <groupId>com.querydsl</groupId>
    <artifactId>querydsl-apt</artifactId>
</dependency>

<dependency>
    <groupId>com.querydsl</groupId>
    <artifactId>querydsl-jpa</artifactId>
</dependency>

<plugin>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-maven-plugin</artifactId>
</plugin>

<plugin>
    <groupId>com.mysema.maven</groupId>
    <artifactId>apt-maven-plugin</artifactId>
    <executions>
        <execution>
            <goals>         
                <goal>process</goal>
            </goals>
            <configuration>
                <outputDirectory>target/generated-sources/java</outputDirectory>
                <processor>com.mysema.query.apt.jpa.JPAAnnotationProcessor</processor>
            </configuration>
        </execution>
    </executions>
</plugin>
```

### Entity (Student)
```java
@Entity
@Getter
@Setter
@ToString
@Table(name = "Student")
public class Student {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;

    private String name;

    @ManyToOne
    private Teacher teacher;

    public Student() {}

    @Builder
    public Student(String name, Teacher teacher) {
        this.name = name;
        this.teacher = teacher;
    }
}
```

### Entity (Teacher)
```java
@Entity
@Getter
@Setter
@ToString(exclude = "students")
@Table(name = "Teacher")
public class Teacher {

    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;

    private String name;

    @OneToMany(mappedBy = "teacher")
    private List<Student> students;

    public Teacher() {}

    @Builder
    public Teacher(String name, List<Student> students) {
        this.name = name;
        this.students = students;
    }

}
```

### TeacherRepositoryCustom
```java
public interface RepositoryCustom {
    List<Teacher>  getTeachers();
}
```

### TeacherRepository
```java
public interface Repository extends JpaRepository<Teacher, Long>, RepositoryCustom { }
```

### RepositoryImpl
```java
public class RepositoryImpl extends QuerydslRepositorySupport implements  RepositoryCustom {

    public RepositoryImpl() {
        super(Teacher.class);
    }

    @Override
    public List<Teacher> getTeachers() {
        QTeacher teacher = QTeacher.Teacher;
        QStudent student = QStudent.Student;

        return from(teacher)
                .leftJoin(teacher.students, student)
                .fetchJoin()
                .distinct()
                .fetch();

    }
}
```