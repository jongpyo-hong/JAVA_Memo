# 스프링 웹 MVC 3

---------------------------------------------------------------------------
### 1. 파일 업로드
- enctype="multipart/form-data"
- MultipartFile 인터페이스
- 파일 업로드 경로 -> URL 연계
  - addResourceHandler

### 2. 프로필
- spring.properties
- @Profiles("환경변수")

    - java 배포파일 - Dspring.profiles.active=real

### 3. 프로퍼티
1) PropertySourcesPlaceholderConfigurer 빈 설정
2) @Value

### 4. 스프링 부트 셋팅

- 의존성 : starter : 자동 셋팅 지원

      1. spring initializr
           - Spring boot dbtool
           - lombok
           - Thymeleaf
           - JDBC Api
           - H2 Database
       
      2. maven repository
           - ojdbc8
           - thymeleaf layout
           - spring boot validation 3.1.0 - scope, version 지우기

- application.properties 설정
  
    
      # 서버 포트 설정
      server.port=3000
      
      # 라이브 리로드 설정
      spring.devtools.livereload.enable=true
      
      # 타임리프 설정
      spring.thymeleaf.cache=false
      spring.thymeleaf.prefix=file:src/main/resources/templates/
      
      # 정적자원(css, js) 설정
      spring.resources.static-locations=file:/src/main/resources/static/
      
      # 스프링 JDBC 설정
      spring.datasource.driver-class-name=oracle.jdbc.driver.OracleDriver
      spring.datasource.url=jdbc:oracle:thin:@localhost:1521:orcl
      spring.datasource.username=BOARD2
      spring.datasource.password=aA123456

      # 파일 업로드 설정
      spring.servlet.multipart.maxFileSize=20MB
      spring.servlet.multipart.maxRequestSize=60MB
      file.upload.path=D:/uploads/

- 인텔리제이 설정
      
      - compile : project auto compile ....
      - advencedsetting : Allow auto-make to start .....
      - editer : fileencoding : utf8 ...

- 크롬 - 라이브 리로드

      - livereload Chrome 패키지 다운로드 -> 핀설정

### 5. Scheduled
1) @EnableScheduling : 스케줄 기능 활성화 (MvcConfig 클래스위 @EnableScheduling)

        @Configuration
        @EnableScheduling
        public class MvcConfig implements WebMvcConfigurer
2) @Scheduled : 스케줄러에 따라 실행될 메서드

       //@Scheduled(cron="0 0 1 * * *") // 새벽 1시 마다
       @Scheduled(cron="*/5 * * * * *") // 5초 마다 실행
       public void process() {
       log.info("5초마다 실행");
       }


### 6. 과제 - 게시판 만들기
1. SQL

    - 게시글 번호 
   
   - 제목
   - 내용
   - 등록일시

