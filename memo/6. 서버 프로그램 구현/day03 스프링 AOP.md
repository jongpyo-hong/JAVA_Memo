# AOP 프로그래밍 (Aspect Oriented Programming)

---------------------------------------------------------------
## 1. 프록시(Proxy)

---------------------------------------------------------------
- Proxy :: 대리하다
    - 데코레이터 패턴에 주로 사용

### 1-1. 팩토리얼 연산
- 팩토리얼 연산 :: !5 -> 5 * 4 * 3 * 2 * 1
- 참조 문서 https://github.com/jongpyo-hong/JAVA_Exam/tree/master/6.%20%EC%84%9C%EB%B2%84%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%A8%20%EA%B5%AC%ED%98%84/spring_study/day02/src/main/java/exam04

## 2. 스프링 AOP 구현

---------------------------------------------------------------
#### 의존성

        - spring-aop - API
        - aspectJweaver

---------------------------------------------------------------
  

        1. @Aspect
            - 공통 기능이 있는 클래스

        2. @Pointcut
            - 적용 범위 패턴 설정

            @Pointcut("execution(* exam05..*(..))") // 프록시(공통 기능이 적용될) 범위
            public void publicTarget() {}

        3. @Around
            - 타겟 메서드를 감싸서 특정 Advice를 실행한다
            @Around("publicTarget()")
                - EnableAspectJAutoProxy : 설정 자동화

            public Object process(ProceedingJoinPoint joinPoint) throws Throwable {}
                - 반환값(Object), 매개변수(ProceedingJoinPoint)가 이미 적용되어 있다.

        4. ProceedingJoinPoint
                - Object proceed() : 핵심기능을 수행하는 메서드
                - Signature getSignature() : 메서드 시그니처 정보를 담고있는 메서드
                - Object getTarget() : 원래 객체
                - Object[] getArgs() : 매개변수로 넘어온 값

        5. org.aspectj.lang.Signature
                - String getName()
                - String toLongString()
                - String toShortString()

        6. execution 명시자 표현식

        7. Advice 적용 순서
              - @Order(1), @Order(2) ...