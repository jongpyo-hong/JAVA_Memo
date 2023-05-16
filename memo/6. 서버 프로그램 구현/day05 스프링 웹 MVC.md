# 스프링 웹 MVC

---------------------------------------------------------------------------
### 1. 스프링 MVC 시작하기
- 의존성

      servlet-api  - 스프링은 웹기술이 아니다, servlet이 필요
      servlet.jsp-api
      spring-webmvc
      lombok

### 2. 스프링 MVC 를 위한 설정

- WebMvcConfigurer 인터페이스


- configureDefaultServletHandling :

        DispatcherServlet 의 매핑 경로를 '/'로 주었을 때, 
        JSP/HTML/CSS 등을 올바르게 처리하기 위한 설정을 추가한다.


- configureViewResolvers


- addResourceHandlers


- @EnableWebMvc : 
            
      스프링 MVC 설정을 활성화한다. 스프링 MVC를 사용하는데 필요한 다양한 설정을 생성


### 3. web.xml 파일에 DispatcherServlet 설정
        
          <?xml version="1.0" encoding="UTF-8"?>
          <web-app version="4.0" xmlns="http://xmlns.jcp.org/xml/ns/javaee"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
          http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd">
            <servlet>
              <servlet-name>dispatcher</servlet-name>
                <servlet-class>
                  org.springframework.web.servlet.DispatcherServlet
                </servlet-class>
              <init-param>
              <param-name>contextClass</param-name>
                <param-value>
                  org.springframework.web.context.support.AnnotationConfigWebApplicationContext // 웹에 특화된 스프링 컨테이너
                </param-value>
              </init-param>
              <init-param>
                <param-name>contextConfigLocation</param-name> // 설정 클래스 설정 
                <param-value>
                    configs.MvcConfig           // 설정 클래스
                    configs.ControllerConfig    // 설정 클래스
                </param-value>
              </init-param>
              <load-on-startup>1</load-on-startup>
            </servlet>

            <servlet-mapping>
              <servlet-name>dispatcher</servlet-name>
              <url-pattern>/</url-pattern>
            </servlet-mapping>

            <filter>
                <filter-name>encodingFilter</filter-name>
                <filter-class>
                    org.springframework.web.filter.CharacterEncodingFilter
                </filter-class>
                <init-param>
                    <param-name>encoding</param-name>
                    <param-value>UTF-8</param-value>
                </init-param>
            </filter>
            <filter-mapping>
                <filter-name>encodingFilter</filter-name>
                <url-pattern>/*</url-pattern>
            </filter-mapping>
          </web-app>

### 4. 코드 구현
- 컨트롤러 구현
- JSP 구현

### 5. 스프링 MVC 프레임워크 동작 방식
1) 스프링 MVC 의 핵심 구성 요소

- DispatcherServlet : 웹에 특화되어 있는 특별한 기능을 가진 스프링 컨테이너

  - 핵심 관리객체

        - HandlerMapping : 요청url과 매칭되는 컨트롤러 검색
          - @Controller 인터페이스
          - HttpRequestHandler 인터페이스
    
        - HandlerAdapter : 모델앤뷰 객체로 변환해서 반환
          - 다양한 요청 처리 빈 -> 처리
        
            - ModelandView : 컨트롤러의 실행 결과를 보여줄 View 검색
                - model : 데이터
                - view : 템플릿 경로

        - VeiwResolver : 요청 처리 결과를 생성할 View를 찾아주고 View는 최종적으로 클라이언트에 응답을 생성해서 전달한다.
          - @RequestParam

<img src="C:\Users\Administrator\Desktop\홍종표_\image\DispatcherServlet.png" width="80%">

#### - 요청 방식
- @GetMapping
- @DeleteMapping


- @PostMapping
- @PutMapping
- @PatchMapping

- @RequestMapping : 요청방식에 상관없이 공통적인 URL을 묶어서 처리할때


### - 커맨드 객체

      - EL 속성으로 자동 추가
      - 클래스명의 앞글자만 소문자로 된 상태로  


- Model model
    - addAttribute(String key, Object value)
  
        -> EL 속성으로 추가(pageContext, request, session, application)

      
- 서블릿 기본 필수 객체 -> 스프링 관리 객체
1) 요청을 처리하는 메서드에 주입
2) @Autowired
    
      - HttpServletRequest
      - HttpServletResponse
      - HttpSession
    