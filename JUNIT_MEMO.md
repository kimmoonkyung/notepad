## TDD
    테스트 주도 개발에서 사용하지만, 
    코드의 유지 보수 및 운영 환경에서의 에러를 미리 방지하기 위해서
    단위 별로 검증하는 테스트 프레임워크

### 단위 테스트
    작성 코드가 기대하는 대로 동작을 하는지 검증하는 절차


### JUNIT
    JAVA 기반의 단위 테스트를 위한 프레임 워크
        Annotation 기반으로 테스트를 지원하며, Assert를 통하여, ( 예상, 실제 )를 통해 검증


### 인텔리제이
    > 새 프로젝트
        > gradle
            > 자바 11
                > build.gradle에 test 관련 디펜던시 추가 및 test { useJUnitPlatform 추가 }
                    > mockito 추가
                        > maver repository
                            > mockito 검색 후 mockito Core / Mockito jUnit Jupiter
                                >  gradle 디펜던시 복사후 build. gralde 붙여넣기
            > Mocking 처리
                > 
    