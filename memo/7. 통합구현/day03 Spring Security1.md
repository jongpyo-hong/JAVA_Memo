# Spring Data JPA

## 1. 연관관계 매핑

-----------------------------------------------------------------------------------------------------------

- @ManyToOne - 다대일

    - 여러 게시글(Many) - 한명의 회원(One)

    - 외래키- Many쪽에 생성 
        - One쪽 엔티티명_기본키 명칭으로 생성
        - @JoinColumn(name="외래키명") - 으로 명칭 변경 가능
        - fetch
            - FetchType
                - .Eager : 즉시로딩 - 처음부터 join : 필요할때만 사용
                - .LAZY : 지연로딩 - 필요할때 쿼리실행 : 글로벌전략(Global)
                        - N + 1 문제가 발생한다
                        - 해결)
                            1) @Query 어노테이션에 JPQL 지정
                            2) QueryDsl fetchJoin()

- @OneToMany - 일대다
    
    - 한명의 회원(One) - 여러 게시글(Many)
    
    - 연관관계의 주인을 명시해야한다
        - mappedBy(name="연관관계 주인")
        - *연관관계 주인 : 엔티티 간의 관계를 결정 지을 수 있는 엔티티 (외래키가 있는 쪽이 주인이다)
            - Many쪽 외래키 - 주인
            - 데이터를 수정 가능한 쪽


- @OneToOne - 일대일

- @ManyToMany - 다대다
    - 중간 테이블 생성

## 2. 영속성 전이

-----------------------------------------------------------------------------------------------------------


* 외래키 제약조건 - 참조 무결성 제약조건

    - @OneToMany
        - cascade

            <table>
                <thead>
                    <tr>
                        <th>CASCADE 종류</th>
                        <th>설명</th>
                    <tr>
                </thead>
                <tbody>
                    <tr>
                        <td>PERSIST</td>
                        <td>부모 엔티티가 영속화될 때 자식 엔티티도 영속화</td>
                    </tr>
                    <tr>
                        <td>MERGE</td>
                        <td>부모 엔티티가 병합될 때 자식 엔티티도 병합</td>
                    </tr>
                    <tr>
                        <td>REMOVE</td>
                        <td>부모 엔티티가 삭제될 때 연된된 자식 엔티티도 삭제</td>
                    </tr>
                    <tr>
                        <td>REFRESH</td>
                        <td>부모 엔티티가 refresh되면 연관된 자식 엔티티도 refresh</td>
                    </tr>
                    <tr>
                        <td>DETACH</td>
                        <td>부모 엔티티가 detach 되면 연관된 자식 엔티티도 detach 상태로 변경</td>
                    </tr>
                    <tr>
                        <td>ALL</td>
                        <td>부모 엔티티의 영속성 상태 변화를 자식 엔티티에 모두 전이</td>
                    </tr>
                </tbody>
            </table>
    



## 3. Spring Security

-----------------------------------------------------------------------------------------------------------


### 1. Spring Security

- 의존성
    - spring boot starter security (버전X)

- 설정
    - formLogin : 3.0 - 메서드 체이닝 방식 / 3.1 - 람다식 방식

- 인증 - 로그인

- 인가 - 접근 권한 통제

- 접속보안(CSRF - Cross Site Request Forge) - 토큰
