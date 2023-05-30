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

## 4. 쿼리 메서드

## 5. @Query 어노테이션

## 6. Querydsl

## 7. 연관 관계 매핑

## 8. 공통 속성화
- 상속을 통한 공통 속성화
- @MappedSuperclass
- 추상 클래스로 정의한다 (테이블을 만들지 않는다)