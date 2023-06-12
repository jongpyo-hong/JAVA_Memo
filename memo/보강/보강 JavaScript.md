# JavaScript


## 1. 웹 브라우저 객체

---------------------------------------------------------------------------------------------

### 브라우저 
- 1. 네이티브 객체(ECMAScript)


- 2. 호스트 객체(런타임 환경(실행 환경)에 따라 다르게 정의된 객체)
        - 웹 브라우저 객체

        - 브라우저에 특화된 객체가 정리 되어있다

        - window (생략 가능)
                - location : 주소와 관련된 기능
                        - hash : # ...
                - history
                - screen
                - navigator
                - document

### 1. 클라이언트 측 자바 스크립트

### 1-1. 웹 브라우저에서 자바스크립트가 하는일


### 1-2. 웹 브라우저에서 자바스크립트 실행순서
        - 서버 응답 (Content-Type: text/html; HTML 텍스트) 
        -> 브라우저 
        -> 번역 
        -> document 객체 변환, Tree 구조로 재구성(DOM Tree, 검색에 용의하다)  
                DOM이 구성되어야만 하위 단계들이 실행된다
        -> DOMContentLoaded 이벤트 발생 (DOM 객체만 구성완료) 
        -> load 이벤트 발생(기타 자원들 로드 완료 - 이미지, css, js ...)

### 1-3. async와 defer 속성

        - defer : DOM 구성이 완료 되면(DOMContentLoaded 이벤트 발생 후) 스크립트 실행
        - async : 비동기 처리

### 1-4. CSS와 렌더링


### 1-5. 웹 브라우저 렌더링 엔진과 자바 스크립트 엔진


## 2. Window 객체

### 2-1. Window 객체의 주요 프로퍼티

        <table>
                <tr>
                        <th>프로퍼티</th>
                        <th>설명</th>
                        <th>메서드</th>
                <tr>
                <tr>
                        <td>screen</td>
                        <td>Screen 객체를 가리킨다.</td>
                </tr>
                <tr>
                        <td>document</td>
                        <td>	Document 객체를 가리킨다.</td>
                </tr>
                <tr>
                        <td>location</td>
                        <td>	Location 객체를 가리킨다.</td>
                </tr>
                <tr>
                        <td>navigator</td>
                        <td>	Navigator 객체를 가리킨다.</td>
                </tr>
                <tr>
                        <td>history</td>
                        <td>History 객체를 가리킨다.</td>
                </tr>
                <tr>
                        <td>event</td>
                        <td>	Event 객체를 가리킨다.</td>
                </tr>
                <tr>
                        <td>console</td>
                        <td>	Console 객체를 가리킨다.</td>
                        <td>.log(), .dir(), .error(), .trace(), .time(), .timeEnd()...</td>
                </tr>
                <tr>
                        <td>window</td>
                        <td>Window 객체를 가리킨다.</td>
                </tr>
                <tr>
                        <td>self</td>
                        <td>Window 객체를 가리킨다(window 프로퍼티와 같음).</td>
                        <td>this == self == window, parent: 부모 창이 없으면 window</td>
                </tr>
                <tr>
                        <td>parent</td>
                        <td>	해당 창이 프레임 안의 창이면 부모 window 객체를 가리킨다. 그렇지 않으면 자기 자신을 가리킨다.</td>
                </tr>
                <tr>
                        <td>top</td>
                        <td>	해당 창이 프레임 안의 창이면 top 레벨의 window 객체를 가리킨다. 그렇지 않으면 자기 자신을 가리킨다.</td>
                </tr>
                <tr>
                        <td>opener</td>
                        <td>	현재 창을 생성한 창을 가리킨다.</td>
                </tr>
                <tr>
                        <td>frames[]</td>
                        <td>	창에 포함된 각 프레임을 가리키는 참조가 저장된 배열</td>
                </tr>
                <tr>
                        <td>closed</td>
                        <td>현재 창이 닫혀 있는지를 뜻하는 논리값</td>
                </tr>
                <tr>
                        <td>name</td>
                        <td>현재 창의 이름(읽기/쓰기 가능)</td>
                </tr>
                <tr>
                        <td>status</td>
                        <td>상태 표시줄의 텍스트(읽기/쓰기 가능)</td>
                </tr>
                <tr>
                        <td>screenX, screenY</td>
                        <td>컴퓨터 화면의 왼쪽 윗부분을 기준으로 했을 때 브라우저 왼쪽 위 꼭지점의 수평 위치와 수직 위치, 인터엣 익스플로러는 지원하지 않는다.</td>
                </tr>
                <tr>
                        <td>screenLeft, screenTop</td>
                        <td>각각 screenX, screenY와 같다. 파이어폭스는 지원하지 않는다.</td>
                </tr>
                <tr>
                        <td>innerHeight, innerWidth</td>
                        <td>창 안쪽의 높이와 너비(스크롤 막대가 차지하는 영역은 제외함)</td>
                </tr>
                <tr>
                        <td>outerHeight, outerWeight</td>
                        <td>창 바깥의 높이와 너비(스크롤 막대가 차지하는 영역을 포함)</td>
                </tr>
                <tr>
                        <td>scrollX, scrollY</td>
                        <td>	수평 방향과 수직 방향으로 HTML 문서가 스크롤되는 픽셀의 수</td>
                </tr>
                <tr>
                        <td>pageXOffset, pageYOffset</td>
                        <td>	각각 scrollX, scrollY와 같다.</td>
                </tr>
        </table>



### 2-2. Window 객체의 주요 메서드

        - Location 객체
        
        - History 객체

        - Navigator 객체

        - Screen 객체

## 3. 창 제어하기

### 1. 창 여닫기

        - open()
        - close()

### 2. 창 제어하기

        - moveTo
        - moveBy
        - resizeTo
        - resizeBy
        -