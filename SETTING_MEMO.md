## mysql 설치
    > brew update
    > brew search mysql
    > brew install mysql
    > brew list
        (home brew로 설치 된 오픈소스들은 /usr/local/Cellar에서 확인)
## mysql 실행 / 종료
    > mysql.server start / stop
        or > brew services start mysql / stop mysql
## mysql workbench 설치
    > brew cask install mysqlworkbench

## workbench에서 스키마 생성
    스키마 탭
        Create Schema > 
            Character Set > utf8mb4 
            Collation > ut8mb4_bin
                Apply


##  스프링 부트면 추가
    application.properties (main/resource/)
        # db source url
        spring.datasource.url=jdbc:mysql://localhost:3306/study?useSSL=false&useUnicode=true&serverTimezone=Asia/Seoul

        # db response name
        spring.datasource.username='DB접속 아이디'

        # db response password
        spring.datasource.password='DB접속 비밀번호'
