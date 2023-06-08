# Spring Data JPA


## 1. Spring Interceptor

---------------------------------------------------------------------------------------------

### 1. Interceptor

- 시점별 공통기능


### *HandlerInterceptor 인터페이스

#### boolean preHandle(...) : 컨트롤러 실행전
        - 공통 수행 내용
        - 통제 : 컨트롤러 실행 통제
            - false : 컨트롤러 실행 X
            - true : 컨트롤러 실행 O
            - 권한 통제(인가)

#### void postHandle(...)
        - 컨트롤러 실행 후 ModelAndView 반환 직후

#### void afterCompletion(...)
        - 응답 완료 후


- 스프링 관리 객체 생성 
    -  -> 설정에(WebMvcConfigurer::addInterceptors) 등록 
    -  -> URL 별 실행하는 인터셉터
