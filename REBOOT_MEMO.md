--Chapter 1. 스프링부트 생성 (maven)
    1. 기본설정 및 Dependency 설정(일단 Web 추가)
    2. 간단한 Rest API Controller 추가
        @RestController
        public class HelloController {
        
            @GetMapping("/api/hello")
            public String hello(){
            
                return "안녕하세요. 현재 서버시간은 "+new Date() + "입니다. \n";
            }
        }
    3. 스프링부트 실행
        > http://localhost:8080/api/hello

--Chapter 2. 리액트 생성
    1. 스프링부트 설치 디렉토리 (ex com.example.demo면 )
       demo/ 디렉토리 터미널에서
       npm create-react-app '폴더명'
        > demo/'폴더명' 생성됨.
    2. 해당 디렉토리 터미널엥서 'yarn start' or 'npm start'
        > 실행 확인
    3. 리액트와 스프링부트의 cors 문제 해결
        생성한 리액트 디렉토리의 package.json을 열어서 proxy 설정값 추가.
            > cmd + k 로 package.json 검색 후
            > "proxy": "http://localhost:8080" 추가
    4. 스프링부트와 리액트 서버 둘다 실행 후.
        > http://localhost:3000/
        > 터미널에서 curl http://localhost:3000/api/hello
            > 정상

--Chapter 3. 리액트의 App.js를 변경해서 Rest API의 값을 받고 출력하기.
    1. App.js 수정
        import React, { useState, useEffect } from 'react'; /* useStae와 useEffect의 개념 확인 */
        import logo from './logo.svg';
        import './App.css';

        function App() {

        const [message, setMessage] = useState(""); /* 이 변수의 의미 확인 */

        useEffect(() => {
            fetch('/api/hello')
            .then(response => response.text())
            .then(message => {
                setMessage(message);
            });
        }, []) /* 마찬가지 확인 */

        return (
            <div className="App">
                <header className="App-header">
                <img src={logo} className="App-logo" alt="logo"/>
                <h1 className="App-title">{message}</h1> /* 이 {message 변수에 Rest API의 값이 들어온다.} */
                </header>
                <p className="App-intro">
                프론트엔드 vscode상에서 수정
                To get started, edit <code>src/App.js</code> and save to reload.
                </p>
            </div>
            )
        }
        export default App;

    2. 서버 실행
       http://localhost:3000/
        > 정상

--Chapter 4. Spring-Boot와 React를 함께 패키징 하기
    1. Maven으로 NPM 실행
        pom.xml에 추가
            /* 디펜던시 (플러그인 or 디펜던시로 추가) */
            <dependency>
                <groupId>com.github.eirslett</groupId>
                <artifactId>frontend-maven-plugin</artifactId>
                <version>1.9.1</version>
            </dependency>

            /* 플러그인 (디펜던시 추가하면 생략해도 될 것 같음) */
            <plugin>
                <groupId>com.github.eirslett</groupId>
                <artifactId>frontend-maven-plugin</artifactId>
                <version>1.9.1</version>
                <configuration>
                    <workingDirectory>frontend</workingDirectory>
                    <installDirectory>target</installDirectory>
                </configuration>
                <executions>
                    <execution>
                        <id>install node and npm</id>
                        <goals>
                            <goal>install-node-and-npm</goal>
                        </goals>
                        <configuration>
                            <nodeVersion>v14.9.0</nodeVersion> /* node -v 버젼 맞추기 */
                            <npmVersion>6.14.8</npmVersion> /* npm -v 버젼 맞추기 */
                        </configuration>
                    </execution>
                    <execution>
                        <id>npm install</id>
                        <goals>
                            <goal>npm</goal>
                        </goals>
                        <configuration>
                            <arguments>install</arguments>
                        </configuration>
                    </execution>
                    <execution>
                        <id>npm run build</id>
                        <goals>
                            <goal>npm</goal>
                        </goals>
                        <configuration>
                            <arguments>run build</arguments>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
    2. 추가 후 maven 업데이트 후 빌드
        com.exaple.demo 면 
        > /demo 터미널에서 ./mvnw clean install
    2-1. 빌드 완료 구문 후 frontend/build/ 폴더 안에 여러가지 파일 생김
    
    3. Spring Boot JAR 파일 안에 프론트엔드 Build 파일 포함 시키기.
        /* 플러그인 */
        <plugin>
            <artifactId>maven-antrun-plugin</artifactId>
            <executions>
                <execution>
                    <phase>generate-resources</phase>
                    <configuration>
                        <target>
                            <copy todir="${project.build.directory}/classes/public">
                                <fileset dir="${project.basedir}/frontend/build"/>
                            </copy> /* 의미 확인 해볼 것 */
                        </target>
                    </configuration>
                    <goals>
                        <goal>run</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    4. 마찬가지로 추가 후 빌드
        com.exaple.demo 면 
        > /demo 터미널에서 ./mvnw clean install
    4-1. 2-1의 파일(frontend/build/)들이 target/classes/public 에도 생성됨.

    5. 빌드 후 /demo/target/ 디렉토리에 jar 파일 생성
        /demo/target/
        > sudo java -jar aaa.jar
        > http://localhost:8080/
            > 리액트 서버에서 뜨던 화면 확인
            > ctrl + c 종료
        > 백그라운드 실행
            > sudo nohup java -jar aaa.jar &

--마무리.
    1. frontend는 vscode에서 개발하고
    2. backend는 intelliJ에서 개발
    3. 후에 빌드
        ./mvnw clean install
    4. 터미널에서 실행
        java -jar aaa.jar
            >http://localhost:8080/

--참고
1. https://github.com/kantega/react-and-spring
2. https://sundries-in-myidea.tistory.com/71