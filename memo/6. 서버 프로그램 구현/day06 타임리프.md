# 타임리프(Thymeleaf)

---------------------------------------------------------------------------
1) 스프링 MVC 와 타임리프 연동 설정


2) 타임리프 소개

    - 의존성

                - thymeleaf-spring5
                - thymeleaf-extras-java8time

-> 식 객체 #temporals


### 타임리프 기본문법
1) 타임리프의 주요 식(expression)

         1) 변수식 : ${속성}

         2) 링크식 : @{링크(url)} 
            - ContextPath가 자동 추가된다
            - Parameter 추가(쿼리스트링 추가) : <a href="#" th:href="@{/member/login(key1=value2, key2=value2)}">
            - 변수 방식으로도 사용 가능 : <a th:href="${/member/info/{id}(id=${joinForm.userId})}">

         3) 메세지 식 : #{메세지 코드} - MvcConfig에서 MessageSource 객체 추가
            - 설정 : MessageSource 빈
                  - 메세지파일(*.properties)

         4) 선택 변수 식 (th:Object="${...}") : *{속성명}

         th:block
            -> 태그 없이 번역
         직접 정의
         [[${변수식}]]
         [[#{키}]]
         [[*{속성}]]
         [[@{링크(url)}]]
               
2) 타임리프 식 객체

- <a href="https://github.com/yonggyo1125/curriculum300H/tree/main/6.Spring%20%26%20Spring%20Boot(75%EC%8B%9C%EA%B0%84)/15~16%EC%9D%BC%EC%B0%A8(6h)%20-%20%ED%83%80%EC%9E%84%EB%A6%AC%ED%94%84(Thymeleaf)/Expression%20Basic%20Objects">Basic Object</a>

- <a href="https://github.com/yonggyo1125/curriculum300H/tree/main/6.Spring%20%26%20Spring%20Boot(75%EC%8B%9C%EA%B0%84)/15~16%EC%9D%BC%EC%B0%A8(6h)%20-%20%ED%83%80%EC%9E%84%EB%A6%AC%ED%94%84(Thymeleaf)/Expression%20Utility%20Objects">Utility Object</a>


   - 커스텀 타임리프

         - ${@스프링빈 이름.메서드명/속성명}
         - *{@스프링빈 이름.메서드명/속성명}
            

3) th:text : 식의 내용을 텍스트로 출력할 때 주로 사용한다

         - th:utext : 식의 내용 중 HTML 도 인식해서 출력한다(기존의 th:text는 html언어를 인식 하지 못함)

4) th:each : 반복문

         - status : 반복 상태에 대한 태그
               - .index : 0부터 시작하는 번호
               - .count : 1부터 시작하는 번호
               - .first : 첫번째
               - .last : 마지막

               - .even : 짝수
               - .odd : 홀수

5) th:if, th:unless : 조건문, !조건문

         -  th:if : 조건식이 참이면 출력, 거짓이면 미출력
         -  th:unless : 조건식이 참이면 미출력, 거짓이면 출력


6) th:href
   
         -> 링크식 @{링크(url)}
                  - 절대경로 ("/로 시작") -> ContextPath
                           view/1 -> /day06/view/1
                  - 상대경로 ("/로 시작X")
                           view/1 -> /day06/board/view/1

7) th:object


8) #temporals : 날짜의 형식(format) 설정 : th:text="*{#temporals.format(regDt, 'yyyy.MM.dd')}"

### 스프링 MVC 폼과 에러 메시지 연동