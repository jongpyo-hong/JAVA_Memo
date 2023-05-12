# 스프링 DI 설정 및 사용

---------------------------------------------------------------
### 1. 스프링을 이용한 객체 조립과 사용


### 2. DI 방식 1 : 생성자 방식


### 3. DI 방식 2 : 세터 메서드


### 4. @Configuration 설정 클래스와 @Bean 설정과 싱글톤
    - @Configuration 설정 : 스프링이 관리할 객체에 대한 설정
    - @Bean : 스프링이 관리할 객체


### 5. 두개 이상의 설정 파일 사용하기


### 6. @Import 애노테이션
    - 여러개의 설정 파일 추가
    - @Import(value={AppCtx2.class}) || @Import(AppCtx2.class)


# *의존 자동 주입*

--------------------------------------------------------------
### 1. @Autowired 애노테이션
    1) 멤버변수

    2) setter 메서드의 매개변수 
        - 매개변수에 의존 객체를 주입하고 호출한다

    3) Optional(Wrapper 클래스)

    4) 생성자 매개변수(기본 생성자가 없을때 사용가능) : @Autowired X

### 2. 일치하는 빈이 없는 경우


### 3. 빈 이름과 기본 한정자


    - @Qualifier 애노테이션


### 4. Autowired 애노테이션의 필수 여부
- @Autowired(required) = @Autowired(required = false)
- 
        - 기본값이 true, 빈이 없으면 오류가 발생한다
        - false -> setter 형태 메서드를 호출하지 않는다
        - 아예 setter 를 호출하지 않는다

- @Nullable

      - setter 메서드를 호출, 의존 객체가 없으면 null 값을 주입한다
# 컴포넌트 스캔

------------------------------------------------------------
### 1. @ComponentScan 애노테이션


### 2. @ComponentScans 애노테이션
    - 정해진 패키지와 하위패키지의 특정 애노테이션이 정의된 클래스를 모두 스프링 관리객체로 생성
    - basePackages
   

### 3. 기본 스캔 대상
    - @Component

    - @Service

    - @Configuration

    - @Controller

    - @RestController

    - @Repository

    - @Aspect

    - @ControllerAdvice

    - @RestControllerAdvice
   

### 4. 컴포넌트 스캔에 따른 충돌 처리
    - excludeFilters
        - @Filter
            - ANNOTATION
            - ASSIGNABLE_TYPE - 클래스, 인터페이스
                    -> classes = ...
            - REGEX
            - ASPECTJ
                - ANT 패턴
                - patterm=".."

                * -> 현재 경로의 모든 파일, 모든 패턴
                ** -> 현재 경로를 포함한 하위 경로의 모든 파일, 모든 패턴
                ? -> 문자 1개

                .* -> 현재 패키지의 하위 클래스
                ..* -> 현재 패키지를 포함한 하위 패키지 포함 하위 클래스

    Spring AOP API
    aspectJweaver

- 빈 이름 충돌

       - Bean이름 -> 첫글자면 소문자로만 만든 클래스명
        

# 빈 라이프 사이클과 범위

------------------------------------------------------------------
#### 1. 객체 생성 -> 의존 설정 주입 -> 초기화 -> 소멸


#### 2. 인터페이스 initializingBean, DisposableBean
- initializingBean

      - afterPropertiesSet () -> 초기화 단계에서 실행 - 객체 생성, 의존성 주입 이후 실행된다 
                              -> 객체에서 실행되는것이 아닌, 스프링 컨테이너 안에서 실행된다

- DisposableBean

      - destroy() -> 소멸 단계에서 실행 (ctx.close() 호출시 실행), 스프링 컨테이너 소멸 전 실행
                  -> 자원해제, ctx.close()가 없으면 실행되지 않는다


#### 3. @Bean
        - initMethod, destroyMethod


# 빈 객체의 생성과 관리 범위

-------------------------------------------------------------------
- ### @Scope

      - singleton : 동일객체
      - prototype : 다른객체