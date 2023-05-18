# 스프링 웹 MVC

---------------------------------------------------------------------------
### 1. 커맨드 객체
- @ModelAttribute
    - 커맨드 객체로 지정할 때 사용한다
    - 커맨드 객체의 이름(EL식 이름)
  
- th:field : HTML 태그에 맞게 값을 넣어주거나 선택하거나, 체크한다

### 2. 리다이렉트

- return "redirect:주소"
  - response.sendRedirect(request.getContextPath() + 주소) 와 같은 기능

          ex)  return "redirect:/member/login";

### 3. 폼 태그

### 4. 모델 

    속성 값을 주입 할 수 있는 객체
    각 Controller에 Model model 을 매개변수로 입력하면 
    model.addAttribute(); 으로 속성을 추가 할 수 있다

### 5. 메시지

    MvcConig내에
        @Bean
        public MessageSource messageSource() { // resources 패키지에 messages 패키지 추가 -> commons.properties 파일 추가
        ResourceBundleMessageSource ms = new ResourceBundleMessageSource();
        ms.setBasenames("messages.commons"); // 확장자를 쓰지 않는다
        ms.setDefaultEncoding("UTF-8");

        빈 객체를 만들면, resources 패키지 안의 messages 패키지에 commons.properties를 사용 가능하다

## 의존성 (데이터베이스)

        - Spring jdbc + Tomcat jdbc
        - jdbcTemplate
        - Slf4j-api / logback-classic
        - Tomcat jdbc
        - ojdbc8

- DataSource - 설정

- PlatFormTransactionManager - @Transactional
### 6. 커맨드 객체 검증

- Validator 인터페이스
- Error 에러 객체 : 요청 메서드와 주입
- 출력하는 템플릿과 연동이 되어있다
  
       - rejectValue(...) : 특정 필드에 한정한 오류 객체 
       - reject : 커맨드 객체 전체에 한정한 오류 객체
        - boolean hasErrors() : 한번이라도 rejectValue, reject가 호출되면

### 7. 세션, 인터셉터, 쿠키

### 8. 날짜 값 변환

### 9. @PathVariable

### 10. 컨트롤러 예외처리