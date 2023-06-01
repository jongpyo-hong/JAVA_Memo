# Spring Data JPA

- 의존성
    
        - springboot devtool
        - Lombok
        - spring web
        - thymeleaf
        - spring data jpa
        - validation
        - h2 database

        - thymeleaf layout
        - ojdbc8

## 1. 동작 방식 
1. JPA란?

        - JPA (Java Persistence API)
              - 자바 영속성 API
              - 영속성 : 상태 감지 메모리
              - jakarta ee
              - 구현체 : hibernate entitymanager
              - 데이터베이스 드라이버 : ojdbc8

        - ORM (Object Relational Mapping)

2. JPA 의 장점
- 특정 데이터베이스에 종속되지 않음

  - 애플리케이션 개발을 위해 데이터베이스로 오라클 oracle을 사용하여 개발을 진행했다고 가정하면, 만약 오라클을 오픈소스인 MariaDB로 변경한다면 데이터베이스마다 쿼리문이 다르기 때문에 전체를 수정해야 한다. 따라서 처음 선택한 데이터베이스를 변경하기 어렵다. 하지만 JPA는 추상화한 데이터 접근 계층을 제공한다. 설정 파일에 어떤 데이터베이스를 사용하는지 알려주면 얼마든지 데이터베이스를 변경할 수 있다.
- 객체지향적 프로그래밍
    
   - JPA 를 사용하면 데이터베이스 설계 중심의 패러다임에서 객체지향적으로 설계가 가능하다. 이를 통해 좀 더 직관적이고 비즈니스 로직에 집중할 수 있도록 도와준다.
    
- 생산성 향상
    
    - 데이터베이스 테이블에 새로운 컬럼이 추가되었을 경우, 해당 테이블의 컬럼을 사용하는 DTO 클래스의 필드도 모두 변경해야 한다. JPA에서는 테이블과 매핑된 클래스에 필드만 추가한다면 쉽게 관리가 가능하다. 또한 SQL문을 직접 작성하지 않고 객체를 사용하여 동작하기 때문에 유지보수 측면에서 좋고 재사용성도 증가한다.


3. JPA 의 단점


4. JPA 동작 방식


5. 설정하기


- DDL AUTO 옵션

      - none : 아무것도 하지 않음
      - create : 서버가 시작되면 기존 테이블 DROP -> 새로 생성(Entity 참고)
      - create-drop : create와 동일하지만, 서버가 종료되기 전에 테이블 DROP
      - update : 변경된 Entity의 구성으로 수정한다(없으면 추가)
      - validate : Entity의 변경 사항만 확인, 변경사항이 있는 경우 예외 발생

        - 개발시 : create, update
        - 실서버 : validate, none

H2 데이터베이스 -> 테스트

### resources -> application.properties

        server.port=3000

        # 타임리프 경로 설정
        spring.thymeleaf.cache=false
        spring.thymeleaf.prefix=file:src/main/resources/templates/
        
        # 정적 자원 경로 설정 (css, js, images)
        spring.resources.static-locations=file:src/main/resources/static/
        
        # 라이브 리로드 (실제 배포시 활성화 x)
        spring.devtools.livereload.enabled=true
        
        # Spring Data JPA 설정
        spring.datasource.driver-class-name=oracle.jdbc.driver.OracleDriver
        spring.datasource.username=JPAEXAMA2
        spring.datasource.password=aA123456
        spring.datasource.url=jdbc:oracle:thin:@localhost:1521:orcl
        
        # 실행되는 쿼리 콘솔 출력
        spring.jpa.properties.hibernate.show_sql=true
        
        # 콘솔 창에 출력되는 쿼리를 가독성 좋게 포맷팅
        spring.jpa.properties.hibernate.format_sql=true
        
        # 쿼리에 물음표로 출력되는 바인드 파라미터 출력
        logging.level.org.hibernate.type.descriptor.sql=trace
        
        spring.jpa.hibernate.ddl-auto=create
        spring.jpa.database-platform=org.hibernate.dialect.Oracle12cDialect

### resources -> application-test.properties

    # Spring Data JPA 설정
    spring.datasource.driver-class-name=org.h2.Driver
    spring.datasource.username=sa
    spring.datasource.password=
    spring.datasource.url=jdbc:h2:mem:test
    
    # 실행되는 쿼리 콘솔 출력
    spring.jpa.properties.hibernate.show_sql=true
    
    # 콘솔 창에 출력되는 쿼리를 가독성 좋게 포맷팅
    spring.jpa.properties.hibernate.format_sql=true
    
    # 쿼리에 물음표로 출력되는 바인드 파라미터 출력
    logging.level.org.hibernate.type.descriptor.sql=trace
    
    spring.jpa.hibernate.ddl-auto=create
    spring.jpa.database-platform=org.hibernate.dialect.H2Dialect


- EntityManagerFactory 객체 -> EntityManager 객체 -> Entity 관리

### 스프링 관리 객체
- EntityManagerFactory 객체 -> EntityManager 객체 : 필요시 의존성 주입

### EntityManager

    - 영속성 컨텍스트(persistence context) : 엔티티를 영구히 저장하는 환경 (상태 변화 감지 메모리)

    - persist(엔티티 객체) : 영속성 상태로 추가(Persistence Context 추가) -> 변화 감지

    - remove(엔티티 객체) : 객체의 영속성 상태를 제거상태로 변경

    - detach(엔티티 객체) : 영속성 분리 : 변화감지 X -> 데이터는 변경하는데, DB에는 반영되지 않는다

    - merge(엔티티 객체) : 영속성이 분리된 엔티티 -> 영속상태 : 변화 감지 상태로 변경

    - find(엔티티 클래스 클래스, 기본키 값) : 영속성 관리되는 엔티티가 있으면 그걸 사용(캐싱), 없으면
      데이터베이스에서 쿼리 후 영속 상태로 보관 -> 조회 (성능상의 이점)

-> 변화 감지는 좋으나 데이터 조회에 한계가 있다

### JPQL (Java Persistence Query Language)
    -> SQL 과 비슷한 문법 -> 조회된 결과 : 영속성 상태


### Spring Data JPA
    -> DAO 클래스를 만들지 않는다
    -> JpaRepository 인터페이스를 사용 -> 구현체는 스프링이 알아서 생성한다(Proxy)



## 2. Entity 설계하기
- 엔티티 매핑 관련 어노테이션


    @Entity : 엔티티 클래스 - 엔티티명 : 클래스명

    @Table : 
            name : 테이블명
            indexes : 인덱스 설정

    - JPA 표준 날짜와 시간 자동 업데이트
        -> 엔티티 상태 변화에 따라 값이 들어간다
        @CreateDate : 처음 엔티티가 영속성에 추가될 때
        @LastModifiedDate : 영속성 상태 변화시
        - 영속성 상태 변화를 감지하는 이벤트 리스너 설정이 필요하다

    참고)
        -> 엔티티 변화 X, 쿼리상
        -> 하이버네이트에서 제공되는 어노테이션
        @CreationTimestamp : INSERT 쿼리시 자동 추가
        @UpdateTimestamp : UPDATE 쿼리시 자동 추가

    @Column 어노테이션
        - 테이블의 필드를 상세하게 설정할 때

        - @column(nullable=true|false) - notnull 제약조건 부여 
        - @columnDefinition)
        - @Column(name="db의 필드명") - 엔티티의 필드명과 실 db의 테이블 필드명이 다를 때
        - @Column(unique="ture|false") - unique 제약조건 부여
        - @Column(length= ) - 기본값 = 255, 컬럼의 길이 설정
        - @Column(insertable=true|false) - 추가 불가
        - @Column(updatable=true|false) - 수정 불가

- 게시글 저장 엔티티
  1. 게시글 번호 - 자동
  2. 게시글 제목
  3. 게시글 내용
  4. 게시글 작성자
  5. 작성일자 - 자동
  6. 수정일자 - 자동
        

## 3. Repository 설계하기
- CrudRepository


- JpaRepository<엔티티 클래스, 기본키가 되는 객체> 인터페이스를 상속 -> Repository

    - 구현체를 proxy 자동생성
    - Dao는 더이상 만들 필요가 없다.
  

    - T save(T t); : em.persist(...), 엔티티를 영속 상태로 추가 
                   : 반환값이 영속 상태에 있는 엔티티
    
    - List<T> saveAll(List<T> list) : 영속성에 여러 엔티티를 한꺼번에 추가

    - T saveAndFlush(T t) : 영속성 추가 -> flush()

    - List<T> saveAllAndFlush(List<T> list) : 영속성에 여러 엔티티를 추가 후 flush()

    - void delete(T t); : em.remove(...)
                        : 엔티티를 영속성 삭제 상태로 추가

    - void flush() : 변화된 상태 -> 실제 데이터베이스에 반영

    - long count(조건식..) : 전체 갯수

    - find : 조회된 결과가 영속성 상태에 있다 - 변화감지
        - findById
        - findAll
        - 앞의 영속성에 추가된 엔티티가 있으면 최종 DB에 반영하고 조회를 해야 하므로 자동으로 flush()가 먼저 실행된다

    - get : 조회된 결과가 영속성 분리 상태에 있다 : 변화감지 X

## 4. 쿼리 메서드
- 쿼리 메서드는 스프링 데이터 JPA에서 제공하는 핵심 기능 중 하나로 Repository 인터페이스에 간단한 네이밍 룰을 이용하여 메서드를 작성하면 원하는 쿼리를 실행할 수 있다.


- 쿼리메서드를 이용할 때 가장 많이 사용하는 문법으로 find를 사용한다. 엔티티의 이름은 생략이 가능하며, By 뒤에는 검색할 때 사용할 변수의 이름을 적어준다.


        find + (엔티티 이름) + By + 변수이름

- 쿼리 메서드 샘플

<table>
    <thead>
        <tr>
            <th>Keyword</th>
            <th>Sample</th>
            <th>JPQL snippet</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>And</td>
            <td>findByLastnameAndFirstname</td>
            <td>... where x.lastname = ?1 and x.firstname = ?2</td>
        </tr>
        <tr>
            <td>Or</td>
            <td>findByLastnameOrFirstname</td>
            <td>	... where x.lastname = ?1 or x.firstname = ?2</td>
        </tr>
        <tr>
            <td>Is, Equal</td>
            <td>findByFirstname<br>
                findByFirstnameIs
                findByFirstnameEquals</td>
            <td>... where x.firstname = ?1</td>
        </tr>
        <tr>
            <td>Between</td>
            <td>findByStartDateBetween</td>
            <td>... where x.startDate between ?1 and ?2</td>
        </tr>
        <tr>
            <td>LessThan</td>
            <td>findByAgeLessThan</td>
            <td>... where x.age < ?1</td>
        </tr>
        <tr>
            <td>LessThanEqual</td>
            <td>findByAgeLessThanEqual</td>
            <td>... where x.age <= ?1</td>
        </tr>
        <tr>
            <td>GreaterThan</td>
            <td>findByAgeGreaterThan</td>
            <td>... where x.age > ?1</td>
        </tr>
        <tr>
            <td>GreaterThanEqual</td>
            <td>findByAgeGreaterThanEqual</td>
            <td>... where x.age >= ?1</td>
        </tr>
        <tr>
            <td>After</td>
            <td>findByStartDateAfter</td>
            <td>... where x.startDate > ?1</td>
        </tr>
        <tr>
            <td>Before</td>
            <td>findByStartDateBefore</td>
            <td>... where x.startDate < ?1</td>
        </tr>
        <tr>
            <td>isNull, Null, isNonNull</td>
            <td>findByAge(is)Null</td>
            <td>... where x.age is null</td>
        </tr>
        <tr>
            <td>NotNull</td>
            <td>findByAge(Is)NonNull</td>
            <td>... where x.age not null</td>
        </tr>
        <tr>
            <td>Like</td>
            <td>findByFirstnameLike</td>
            <td>... where x.firstname like ?1</td>
        </tr>
        <tr>
            <td>NotLike</td>
            <td>findByFirstnameNotLike</td>
            <td>... where x.fistname not like ?1</td>
        </tr>
        <tr>
            <td>StartingWith</td>
            <td>findByFirstnameStartingWith</td>
            <td>... where x.firstname like ?1 (parameter bound with appended %)</td>
        </tr>
        <tr>
            <td>EndingWith</td>
            <td>findByFirstnameEndingWith</td>
            <td>... where x.firstname like ?1 (parameter bound prepended %)</td>
        </tr>
        <tr>
            <td>Containing</td>
            <td>findByFirstnameContaining</td>
            <td>... where x.firstname like ?1 (parameter bound wrapped in %)</td>
        </tr>
        <tr>
            <td>OrderBy</td>
            <td>findByAgeOrderByLastnameDesc</td>
            <td>... where x.age = ?1 order by x.lastname desc</td>
        </tr>
        <tr>
            <td>Not</td>
            <td>findByLastnameNot</td>
            <td>... where x.lastname <> ?1</td>
        </tr>
        <tr>
            <td>In</td>
            <td>findByAgeIn(Collection < Age > ages) </td>
            <td>... where x.age in ?1</td>
        </tr>
        <tr>
            <td>NotIn</td>
            <td>findByAgeNotIn(Collection < Age > ages)</td>
            <td>... where x.age not in ?1</td>
        </tr>
        <tr>
            <td>True</td>
            <td>findByActiveTrue()</td>
            <td>... where x.active = true</td>
        </tr>
        <tr>
            <td>False</td>
            <td>findByActiveFalse()</td>
            <td>... where x.active = false</td>
        </tr>
        <tr>
            <td>IgnoreCase</td>
            <td>findByFirstnameIgnoreCase</td>
            <td>... where UPPER(x.firstname) = UPPER(?1)</td>
        </tr>
    </tbody>
</table>


## 5. @Query 어노테이션
- JPQL을 바로 작성 : 복잡한 쿼리 직접 작성
    - 쿼리의 문법 오류를 실행시에만 알 수 있고, 유지 보수에 좋지 않다.


- 쿼리빌더 : 자바 코드 수준에서 JPQL 완성
    - 오류 여부를 즉각적으로 알 수 있다.
    - 개발자의 문법 오류 실수를 방지한다.
      - jakarta.persistence.criteria : 너무 복잡해서 잘 사용하지 않는다.
      - 비표준 라이브러리 - querydsl : select 구문에 특화 되어있는 쿼리 라이브러리
      - Pageable : 페이징 관련 인터페이시
        - static PageRequest.of(int page(한페이지), int size(몇개씩))
        - static PageRequest.of(int page, int size, Sort sort)

      - PageRequest.of(int page, int size, Sort sort);
      - Sort -> 정렬

## 6. Querydsl
- 쿼리 빌딩을 할 수 있는 클래스를 자동 생성
    (Q엔티티명.java)


- 의존성

      - querydsl jpa
      - querydsl apt : 쿼리 빌딩 클래스 자동 생성 라이브러리
            - 의존성 주입후 <classifier>jakarta</classifier> 추가

      - plugin : apt-maven-plugin

      - com.mysema.maven (plugin) : <plugins>안에 주입</plugins>
            <version>1.13<version> 아래 쪽에
            <executions>
  				<execution>
  					<goals>
  						<goal>process</goal>
  					</goals>
  					<configuration>
  						<outputDirectory>target/generated-sources/java</outputDirectory>
  						<processor>com.querydsl.apt.jpa.JPAAnnotationProcessor</processor>
  					</configuration>
  				</execution>
  			</executions> 작성

- 메서드

      - eq(...) : ==
        - lt(...) : <
        - le(...) : <=
        - gt(...) : >
        - ge(...) : >=
        - in(Collection<T> ...)
        - contains - LIKE %:key:%
        - startWith - LIKE ...%
        - endWith - LIKE %...

      - 조건식이 한개 일때는 Q클래스 에서 바로 predicate를 생성
      - 조건식이 여러개 일때는 BooleanBuilder : Predicate 구현
      - 클래스
          - BooleanBuilder : 논리연산자를 처리하는 빌더, 메서드 체이닝으로 여러가지 조건(and, or, not) 부여 가능
            - and
            - or
            - not

## 7. 연관 관계 매핑
- 연관 관계 매핑의 종류

      - 다대일(N:1) : @ManyToOne
            - 게시글 여러개(BoardData) : 회원 1명(Member)
            - Many쪽에 외래키 추가

      - 일대다(1:N) : @OneToMany
            - 회원 1명 : 다수의 게시글
            - mappedBy: 연관관계 주인 명시
            - *연관관계 주인 : 관계를 좌지우지 할 수 있는 엔티티, Many에 외래키가 있기에 관계의 주인은 Many

      - 일대일(1:1) : @OneToOne
      - 다대다(N:N) : @ManyToMany

      - 외래키 -> Many : 엔티티명_기본키명 (member_user_no)
      - @JoinColumn(name="외래키 필드명") : 외래키 필드 이름 설정

## 8. 영속성 전이

## 9. 지연로딩

## 10. 공통 속성화
- 상속을 통한 공통 속성화
- @MappedSuperclass
- 추상 클래스로 정의한다 (테이블을 만들지 않는다)
- Auditing을 이용한 엔티티 공통 속성화


* lombok
  * toString : getter를 통해서 조회후 출력
    - BoardData -> 출력(toString) -> getMember -> toString -> boardDatas -> toString -> getMember().....
    -> 에러발생

  - 해결
  - getter를 사용하지 않고 toString을 직접 멤버 변수로 변경
  - OneToMany 항목, ManyToOne 으로 연결된 항목 toString 제외