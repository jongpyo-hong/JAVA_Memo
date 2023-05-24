# JSON 응답과 요청 처리

---------------------------------------------------------------------------
### 1. JSON 이란?
- JSON (JavaScript Object Notation) : 자바 스크립트 객체 표기법
    
      ex) {"키" : "값", "키" : "값"}

### 2. Jackson 의존 설정
- 의존성 : (*boot 에서는 자동적으로 주입이 되어있다.)

      - Jackson databind
      - Jackson datatype jsr310
        
        -> 자바 객체 -> JSON 문자열로 변환
        -> JSON 문자열 -> 자바 객체로 변환

### 3. @RestController
- JSON 으로 응답, 요청을 받을 수 있는 컨트롤러
- 응답헤더 : Content-Type = application/json
- 문자열 반환 : Content-Type = text/plain

### 4. @ResponseBody
- 일반 컨트롤러(@Controller)에서 JSON 으로 응답 할때

### 5. @JsonIgnore
- JSON 변환 제외 항목을 지정한다

### 6. @JsonFormat
- 날짜, 시간의 형식을 변경(응답, 요청)할 때 사용한다

### 7. @RequestBody
- ARC(Advanced Rest Client) : 테스트 툴 -> 요청, 응답 테스트
  (arc-setup.exe)
- 요청 데이터의 형식이 application/json 형식임을 알려주는 애너테이션

### 8. ResponseEntity< T >
- 응답 상태 코드 + 응답 바디 데이터를 상세하게 통제할 때 사용한다

      - static status(...) : 응답 상태 코드
          - HttpStatus : 응답 코드 Enum 상수가 정의되어 있다

      - body(T body) : 응답 바디 데이터

      - build() : 응답 바디 데이터가 없는 경우

- 자주 사용 되는 응답 코드는 편의 메서드가 정의되어 있다

      - accepted() - 202
      - created(URL..) - 201
      - badRquest() - 400
      - internalServerError() - 500
      - noContent()  - 204
      - notFound() - 404
      - ok() - 200 응답바디가 없을 경우
      - ok(T body) - 200 응답바디가 있을 경우

### 9. @ExceptionHandler
- @RestControllerAdvice


- Jackson Databind

  - ObjectMapper
      - readValue : JSON 문자열 -> Java 객체로 변환
      - writeValueAsString(...) : Java 객체 -> JSON 문자열로 변환
        (Java DTO(Data Transfer Object) 객체만 변환 가능)


- 에러, 성공 데이터 응답의 통일성
  - JSONResult


### 10. 빌더 패턴
- getter, setter 를 대신할 수 있는 패턴
- 객체를 직접 생성하지 않는다, 생성자 접근 제어자가 private