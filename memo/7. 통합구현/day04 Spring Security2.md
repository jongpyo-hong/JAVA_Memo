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


- 로그인한 회원의 정보 조회 방법

    - 컨트롤러 요청 메서드에 주입

        1) Principal principal 주입
                - String getName(); : 로그인한 아이디

        2) @AuthenticationPrincipal UserDetails 구현 객체

    - 주입 없이 바로 조회

        3) SecurityContextHolder
                    .getContext()
                    .getAuthentication() : Authentication
                    .getPrincipal(); 


- 스프링 부트 오류 페이지

    - templates 
       - errors
            - 401.html - 401 오류 발생시
            - 403.html
            - 404.html
            - 500.html
            
            - path : 에러가 발생한 URL 경로
            - status : 응답 코드
            - timestamp : 응답 발생 일시(Epoch Time)
            - error : 에러 메세지
            - errors : 에러 메세지들
            - exception : 예외 객체
            - message : 에러 메세지
            - trace : 자세한 정보


### 타임리프 + 스프링 시큐리티6 - 확장 기능
    - 스프링 시큐리티 + JPA -> 수정자 (로그인한 회원 - 작성자, 수정자 - 자동 추가)


### 2. 인터페이스 명세서