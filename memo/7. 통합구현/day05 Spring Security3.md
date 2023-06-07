# Spring Data JPA


## 1. Spring Security

-----------------------------------------------------------------------------------------------------------

### 1. Spring Security


            - 의존성
                - spring boot starter security (버전X)

            - 설정
                - formLogin : 3.0 - 메서드 체이닝 방식 / 3.1 - 람다식 방식

### - UserDetails 인터페이스 : 회원정보 + 권한
    - ex) User 구현 클래스 - username, password (MemberInfo)

### - UserDetailsService 인터페이스
    - username 값(- 세션, userId) : 회원정보 조회 (MemberInfoService)


- _csrf : 토큰 - 처리 페이지(POST) 에서 검증(요청 header)
            - 검증 실패 (403) 접근 불가

        - ajax : 


- 권한 : authority


### 로그인한 회원의 정보 조회 방법

    - 컨트롤러 요청 메서드에 주입

        1) Principal principal 주입
                - String getName(); : 로그인한 아이디

        2) @AuthenticationPrincipal UserDetails 구현 객체

    - 주입 없이 바로 조회

        3) SecurityContextHolder
                    .getContext()
                    .getAuthentication() : Authentication
                    .getPrincipal(); 


### 타임리프 + 스프링 시큐리티 - 확장기능

- 의존성
    -   <dependency>
            <groupId>org.thymeleaf.extras</groupId>
            <artifactId>thymeleaf-extras-springsecurity6</artifactId>
        </dependency>

- 스프링 데이터 JPA + 스프링 시큐리티 
    - 수정자(로그인한 회원정보 - 추가, 수정시 자동 반영)
    - AuditorAware 인터페이스 : 설정 항목


### 2. 인터페이스 명세서
    - REST API
    - 게시판이 구현된 소스 제공

- 통합구현 Test
    - arc 사용

- @RestControllerAdvice
- @ExceptionHandler


### 3. 통합 테스트 
- MockMvc : 스프링에서 제공되는 테스트 툴

    - MockMvcRequestBuilders : 요청 관련 테스트 기능들
    
    - MockMvcResultMatchers : 요청후 검증에 관한 기능들
            - andExpect(...)

    - MockMvcResultHandlers  : 
            - andDo(...) - print() : 요청과 응답에 대한 자세한 정보