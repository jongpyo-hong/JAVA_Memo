# jdbcTemplate, 트랜잭션

---------------------------------------------------------------
### 1. JdbcTemplate 프로그래밍의 단점을 보완

    - JDBC(Java DataBase Connectivity) API(Application Programming Interface)

### 2. 커넥션 풀 + Tomcat JDBC(Hikari CP ...)

    * 커넥션 풀 : 데이터베이스 연결을 미리 여러개 생성해 높은 저장소
        
        - 의존성 : spring-context - <properties> 안에 <spring.version>5.3.27
                  spring jdbc
                  tomcat jdbc (커넥션 풀) - 사용하는 tomcat 버전이랑 같은 버전
                  ojdbc8 (오라클)

### 3. DataSource 설정

    - 데이터베이스 연결
    - 스프링 관리 객체(@Bean)
    - 커넥션 풀 설정

    - EXAMPLE
        - DataSource ds = new DataSource(); // 커넥션 풀 객체 생성
        ds.setDriverClassName("oracle.jdbc.driver.OracleDriver"); // 데이터베이스 설정
        ds.setUrl("jdbc:oracle:thin:@localhost:1521:orcl"); // 서버 설정
        ds.setUsername("SCOTT"); // 계정 설정
        ds.setPassword("tiger"); // 설정한 계정 비밀번호
        ds.setInitialSize(2); // 커넥션 풀을 초기화할 때 생성할 초기 커넥션 개수를 지정
        ds.setMaxActive(10); // 커넥션 풀에서 가져올 수 있는 최대 커넥션 개수를 지정, 기본값은 100

        ds.setTestWhileIdle(true); // 테스트 설정 (true, false)
        ds.setMinEvictableIdleTimeMillis(30000); // 최대 유휴 시간
        ds.setTimeBetweenEvictionRunsMillis(3000); // 테스트 주기
        return ds;

### 4. Tomcat JDBC 의 주요 프로퍼티

    - ds.setTestWhileIdle(true); // 테스트 설정 (true, false)
    - ds.setMinEvictableIdleTimeMillis(30000); // 최대 유휴 시간
    - ds.setTimeBetweenEvictionRunsMillis(3000); // 테스트 주기

### 5. JdbcTemplate 를 이용한 쿼리 실행

    - int update(...) : INSERT, UPDATE, DELETE 문에 쓰인다.
            - 반환값 : 반영된 레코드 갯수
    - List<T> query(...) : SELECT 문에 쓰인다.
            - 반환값 : 조회된 레코드 (여러개)
    - T queryForObject(...) : SELECT 문에 쓰인다
            - 반환값 : 조회된 레코드 (단일 레코드) 한개
              - 레코드가 1개가 아니면 예외 발생

    - PreparedStatementCreator
        - PreparedStatement
            -> 자동 증감번호(PK)
              - KeyHolder


    - 로그?
    - 의존성
    slf4j-api
    logback-classic

- logback. xml
  - resources 내의 logback.xml

          <?xml version="1.0" encoding="UTF-8" ?>

          <configuration>
              <appender name="stdout" class="ch.qos.logback.core.ConsoleAppender">
                  <encoder>
                      <pattern>%d %5p %c{2} - %m%n</pattern>
                  </encoder>
              </appender>
              <root level="INFO">
                  <appender-ref ref="stdout" />
              </root>
        
              <logger name="org.springframework.jdbc" level="DEBUG" />
          </configuration>

             FATAL
             ERROR
             WARN
             INFO
             DEBUG
             TRACE
      
             *lomboc 라이브러리
                setter, getter
                생성자
                toString
    
                - 주요 애너테이션
                    - @Getter
                    - @Setter
                    - @ToString
    
                    - @ALLArgsConstructor : 모든 멤버변수를 초기화 하는 생성자
                    - @NoArgsConstructor : 기본 생성자
                    - @RequiredArgsConstructor : 반드시 초기화가 필요한 멤버변수를 생성자 매개변수 추가
                                            - 멤버변수가 (final)상수, 초기화X
                                            - @NonNull
    
                    - @Data
                            - @Getter, @Setter, @ToString, @NoArgsConstructor
    
                    - @Builder
                    - ResultSet
                            -> 조회된 레코드 데이터(1개의 레코드)

### 6. PreparedStatementCreator 를 이용한 쿼리 실행
    
-    6-1) 시퀀스 생성 DB -> CREATE SEQUENCE EMP_SEQ;

### 7. INSERT 쿼리 실행 시 KeyHolder 를 이용해서 자동 생성

  - Connection conn
        - PrepareStatement prepareStatement(String sql, ...)

          void set자료형(순서, 값);


### 8. 스프링의 익셉션 변환 처리

- SQLException -> DataAccessException(RuntimeException)

### 9. @Transactional : 트랜잭션 수동 관리 설정
-   클래스명 -> 모든 메서드
-   특정 메서드


      - PlatformTransactionManager
      - DataSourceTransactionManager


    - setAutoCommit(false) - 공통 기능

    - 쿼리수행1 - 핵심기능
    - 쿼리수행2
    ...

    - commit(); - 공통 기능

## 10. 과제

      - https://github.com/jongpyo-hong/assignment_a2.git

- JDBC API
- DB 연결
- 추가, 수정, 삭제 - 3
- 조회 -1

위 4개의 기능을 PrepareStatement 방식으로 정의하기

- 브랜치명 - jdbc_exam

# 스프링 웹 MVC

------------------------------------------------------------------

### 1. 스프링 MVC 시작하기