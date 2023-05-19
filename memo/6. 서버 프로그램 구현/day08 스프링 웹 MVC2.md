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

### 3. 날짜 값 변환

### 4. @PathVariable

### 5. 컨트롤러 예외처리

### 6. 파일 업로드

### 7. 프로필
    - @Profile
    - spring.profiles.active

### 8. 프로퍼티 파일

- PropertySourcesPlaceholderConfigurer