# 스프링 웹 MVC

---------------------------------------------------------------------------
### 1. 커맨드 객체 검증
1) Validator 인터페이스

            - supports(...) : 검증에 대한 커맨드 객체 제한
            - validate(...) : 검증
        
2) Errors 객체

            - 커맨드 객체 자체 오류, 예외
                - reject(String code); // *String code = 커맨드 객체
                - reject(String code, String defaultMessage);
                    - defaultMessage -> 메세지 파일에 code가 정의X

            - 특정 필드에 해당하는 오류, 예외
                - rejectValue(String field, String code);
                - rejectValue(String field, String code, String defaultMessage);

3) 스프링 메세지
- 메세지 - 검증 -> 범위 축소
   
         - 메세지코드.필드명
         - 메세지코드.커맨드객체명.필드명
         - 메세지코드.자료형
         - 메세지코드.필드명.자료형
         - 메세지코드.커맨드객체명.자료형

4) ValidationUtils

        - rejectIfEmpty
        - rejectIfEmptyOrWhitespace

5) Bean Validation Api (자바 표준 - javax.validation 패키지)

        - 구현체 : hibernate validator 

        - 의존성 : bean validation api 
                  hibernate validator

6) @Valid : 스프링에게 검증을 위임한다
   
        - public String joinPs(@Valid JoinForm joinForm, Errors errors)
        - Errors 변수가 반드시 뒤에 와야한다

        1) Bean Validation 으로 검증
        2) 검증이 더 필요한 부분은 Validator 에 직접 구현
7) lombok
    - @RequiredArgsConstructor
   
      : 반드시 값이 있어야 하는 멤버 변수를 생성자 매개변수로 자동 추가
      
            - final 로 정의(상수) - 초기화가 안되어 있는경우
            - @NonNull
8) 암호화
- 양방향 암호화 : 암호화 < - > 복호화
   

- 단방향 암호화 : 암호화 // 복호화 불가 - 해시
      
   - 고정해시 : 같은값 - 같은해시(md5, sha1, sha256, sha512 ...)
   - 유동해시 : 같은값 - 생성시 마다 다른 해시(bcrypt)
  
- 의존성
      
      - Maven Central 페이지 -> jbcrypt0.4
   
 
### 2. 세션, 인터셉터, 쿠키
- 서블릿 핵심 객체 : 편의상 스프링 관리 객체로 추가 되어있다(의존성 자동주입 가능)

    - HttpServletRequest, HttpServletResponse, HttpSession
    - 요청메서드에 주입한다
    - @Autowired

    - @CookieValue -> 쿠키값을 주입한다

#### - 인터셉터

        - boolean prohandle(...)
            : 요청 처리전 공통 기능
            : 통제 제어
                - 반환값이 false : 컨트롤러 빈, 요청 메서드 실행 X
                - 반환값이 true : 컨트롤러 빈 실행, 요청 메서드 실행

        - void postHandle(...)
            : 요청 처리 후 ModelAndView 반환 직후 공통기능

        - void afterCompletion(...)
            : 응답완료 후 공통기능

- WebMvcConfigurer 
    - addInterceptors(...) : 인터셉터 설정 메서드

### 3. 날짜 값 변환
- 커맨드 객체 날짜 -> 문자열
- 형식을 명시하지 않으면 오류 발생 (java.time.*)
- 형식 명시
  - @DateTimeFormat
    - pattern="패턴"
    
            - @DateTimeFormat(pattern = "yyyy-MM-dd")
  
            - 에러 메시지 : typeMismatch.java.time.LocalDate=날짜 형식이 올바르지 않습니다 (ex) 2023-05-20)

    
- 형식 검증 실패 -> typeMismatch 메세지 코드

### 4. @PathVariable - 경로 변수

            @GetMapping("/info/{id}") // {...} : 중괄호 안쪽에 입력하면 경로 변수가 된다
            public String info(@PathVariable(required = false, name = "id") String userId) { 
            // 경로변수를 사용하려면 매개변수가 경로변수와 같아야한다
            // 경로변수가 매개변수와 다르다면 @PathVariable(name="경로변수") name 에 경로변수값을 넣으면 된다
                                                                                    
            System.out.println(userId);
            return "member/info";
            }

### 5. 컨트롤러 예외처리

- @ExceptionHandler 
        
    - 발생할 수 있는 Class 클래스
    - 에러페이지에 대한 설정
  
  * 처리 메서드에 주입 가능한 객체

          - 발생한 예외 객체
          - 서블릿 기본 객체
              (HttpServletRequest, HttpServletResponse, HttpSession ...)
          - Model model

- @ControllerAdvice : 공통 컨트롤러

    - 적용 우선순위
        
        - @Controller > @ControllerAdvice

### 6. 파일 업로드
- 설정 : 파일 1개의 최대 용량, 전체 최대 용량 설정 - (web.xml)

            <multipart-config>
            <max-file-size>20971520</max-file-size> <!-- 20MB -->
            <max-request-size>62914560</max-request-size> <!-- 60MB -->
            </multipart-config>
- MultipartFile 인터페이스


- enctype="multipart/form-data : 양식에 속성으로 추가해야 요청헤더의 데이터가 바뀐다
    
    - multipart -> 양식 데이터 파트, 파일 데이터 파트
  
            - <form method="post" th:action="@{/file/upload}" enctype="multipart/form-data">
    - 정적 경로 설정
    
        - WebMvcConfigurer :: addResourceHandlers

### 7. 프로필
    - @Profile
    - spring.profiles.active

### 8. 프로퍼티 파일

- PropertySourcesPlaceholderConfigurer