서버 관리를 위한 툴 ?

--동작중인 컨테이너  확인
docker ps

--정지된 컨테이너 확인
docker ps -a

--컨테이너 삭제
docker rm [컨테이너id]

--컨테이너 복수 삭제 가능
docker rm [컨테이너id], [컨테이너id]

--컨테이너 모두 삭제
docker rm `docker ps -a -q` 

--현재 이미지 확인
docker images

--이미지 삭제
docker rmi [이미지id]

--컨테이너를 삭제하기 전에 이미지를 삭제할 경우
docker rmi -f [이미지id]

--logs 명령어
docker logs [OPTIONS] CONTAINER
    -> OPTIONS 
        -> docker logs -f [id] (-f : 실시간)
docker logs [id]

--도커 정지 컨테이너 시작
    -> docker container ls -a
    -> docker container start [name]
    -> docker ps 

--도커 컨테이너 정지
    -> docker stop [컨테이너id]

--pull
docker pull ubuntu:18.04

--network create 명령어
docker network create [OPTIONS] NETWORK
    -> 도커 컨테이너끼리 이름으로 통신할 수 있는 가상 네트워크를 만든다.
        -> docker network create app-network2
        -> app-network 라는 이름으로 wordpress와 mysql이 통신할 네트워크를 만듬.
--network connect 명령어
docker network connect [OPTIONS] NETWORK CONTAINER
    -> 기존에 생성된 컨테이너에 네트워크를 추가.
        -> docker network connect app-network2 mysql
        -> mysql 컨테이너에 네트워크를 추가.
            docker run -d -p 8080:80 \
            --network=app-network2 \
            -e WORDPRESS_DB_HOST=mysql \
            -e WORDPRESS_DB_NAME=test \
            -e WORDPRESS_DB_USER=test \
            -e WORDPRESS_DB_PASSWORD=test \
            wordpress
        -> 워드프레스 네트워크연결

--network 목록 명령어
docker network ls
--network 삭제 명령어
docker network rm 'id'

--volume mount 명령어(-v)
docker stop mysql
docker rm mysql
docker run -d -p 3306:3306 \
 -e MYSQL_ALLOW_EMPTY_PASSWORD=true \
 --network=app-network2 \
 --name mysql \
 -v /Users/kimmoonkyung/Documents/mysql:/var/lib/mysql \
 mysql:5.7
    
    -> docker run -d -p 3306:3306 \
    -e MYSQL_ALLOW_EMPTY_PASSWORD=true \
    --network=app-network \
    --name mysql \
    mysql:5.7
        -> localhost:8080 접속시 db 연결 실패로 나옴.

--도커 실행 되어 있지 않을 때 에러
Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?
    -> ps -ef | grep docker 혹은 docker info 
        -> 데몬 실행 명령어를 좀 확인해봐야겠음.
        -> 도커 앱 실행하니 일단 됨.

--도커 설치 확인 및 버젼 확인 명령어
docker version

--도커 기본 명령어 run - 컨테이너 실행
-d detached mode (백그라운드 모드)
-p 호스트와 컨테이너의 포트를 연결
-v 호스트와 컨테이너의 디렉토리를 연결
-e 컨테이너 내에서 사용할 환경변수 설정
--name 컨테이너 이름 설정
--rm 프로세스 종료시 컨테이너 자동제거
-it -i와 -3306yt를 동시에 사용한 것으로 터미널 입력을 위한 옵션
    -> 컨테이너 내부에 들어가기 위해 sh를 실행하고 키보드 입력을 위한 옵션
--network 네트워크 연결

--ubuntu 20.04 컨테이너 만들기
docker run ubuntu:20.04
-> 이미지 있는지를 확인 후 다운로드 함.
-> 이 명령어는 실행만하고 다른 명령어를 주지 않았기 때문에 실행 후 바로 종료됨.
-> 'docker run --rm -it  ubuntu:20.04 /bin/sh' 
    -> 터미널 쉘 실행 후 종료함과 동시에 컨테이너를 삭제처리 하겠다,(-rm 옵션) 일회용품 같은 느낌
    -> rm 옵션이 없다면 컨테이너가 종료되더라도 삭제되지 않고 남아있어서 수동으로 삭제해야함.

--CentOS 실행
docker run --rm -it centos:8 /bin/sh

--웹 어플리케이션 실행하기
docker run --rm -p 5678:5678 hashicorp/http-echo -text="hello world"
    -> localhost:5678 접속 시 hello world 확인 가능 

--redis 실행
docker run --rm -p 1234:6379 redis
    -> telnet localhost 1234

--mysql 실행
docker run -d -p 3306:3306 \
    -e MYSQL_ALLOW_EMPTY_PASSWORD=true \
    --name mysql \
    mysql:5.7

    -> docker: Error response from daemon: Conflict. The container name "/mysql" is already in use by container "168dae7a56d1e6ed834aa5150c9dd42a339c1541d2f0056c73cdbbb3f3177d09". You have to remove (or rename) that container to be able to reuse that name.
    See 'docker run --help'.
    'docker container ls -a '
        -> 이미 실행중이여서 해당 에러메시지 나옴.
        -> docker stop id
        -> docker rm id
        -> 재실행

--mysql 실행
docker exec -it mysql mysql
create database test CHARACTER SET utf8;
grant all privileges on test.* to test@'%' identified by 'test';
flush privileges;
quit 

--워드프레스 블로그 실행
docker run -d -p 8080:80 \
 -e WORDPRESS_DB_HOST=host.docker.internal \
 -e WORDPRESS_DB_NAME=wp \
 -e WORDPRESS_DB_USER=wp \
 -e WORDPRESS_DB_PASSWORD=wp \
 wordpress
    -> docker exec -it mysql mysql
    -> show databases;
    -> use wp
    -> show tables;
    -> select * from wp_users;


--*docker compose
docker-compose.yml 설정 후
    -> docker-compose up -d (시작)
    -> docker-compose down  (종료)

--이미지 만들고 배포.
이미지란
도커는 레이어드 파일 시스템 기반
ex) AUFS, BTRFS, Overlayfs, ...
이미지는 프로세스가 실행되는 파일들의 집합(환경)
프로세스는 환경(파일)을 변경할 수 있음
이 환경을 저장해서 새로운 이미지 파일을 만든다.

--예시 - git 설치
docker run -it --name git ubuntu:latest bash
    -> ubuntu:latest 설치후 git 설치 확인
    -> root@afafaafa:/# git
        -> git: command not found
    -> apt-get update
    -> apt-get install -y git
    -> git --version
        -> 깃 버전 2.17.1
-> 10.05 공부시 docker run -it --name git ubuntu:latest bash
    > 실행 했는데 docker: Error response from daemon: Conflict. 
    > 해당 에러는 이미지 busy box를 삭제 할 때에 
    > 어떠한 컨테이너가 이미 삭제할 이미지를 참조중이기 때문에
    > (컨테이너의 실행 유무는 상관없이) 발생하는 에러 
-> docker container ls -l 로 해당 컨테이너 id 확인 후
-> docker rm 컨테이너id 로 삭제. 
    -> 참조 (https://stackoverflow.com/questions/31676155/docker-error-response-from-daemon-conflict-already-in-use-by-container)

-> docker run -it --name git2 ubuntu:git bash
    > 전단계와 달리 git이 설치되어있음

--도커 이미지 만들기 (build)
docker build -t mxxnkyung/ubuntu:git01 .
명령어          이름공간 이미지이름:태그 빌드컨텍스트

--dockerfile
도커 이미지를 만들기 위해서 dockerfile 이라는 명령어 사용
FROM 기본이미지
RUN 쉘 명령어 실행
CMD 컨테이너 기본 실행 명령어 (Entrypoint의 인자로 사용)
EXPOSE 오픈되는 포트 정보
ENV 환경변수 설정
ADD 파일 또는 디렉토리 추가. URL/ZIP 사용 가능
COPY 파일 또는 디렉토리 추가
ENTRYPOINT 컨테이너 기본 실행 명령어
VOLUME 외부 마운트 포인트 생성
USER RUN, CMD, ENTRYPOINT를 실행하는 사용자
WORKDIR 작업 디렉토리 설정
ARGS 빌드타임 환경변수 설정
LABEL key - value 데이터
ONBUILD 다른 빌드의 베이스로 사용 될 때 사용하는 명령어

--dockerignore
.dockerignore 파일 생성

--Dockerfiles 작성 (이미지 만들기)
-- https://docs.docker.com/engine/reference/builder/
COPY 파일 또는 디렉토리 추가
    > COPY index.html /var/www/html/
    > COPY ./app /usr/src/app
RUN 명령어 실행
    > RUN apt-get update
    > RUN npm install
EXPOSE 컨테이너에서 사용하는 포트 정보
    > EXPOSE 8000
CMD 컨테이너 생성시 실행할 명령어
    > CMD ["node","app.js"]
    > CMD node app.js
WORKDIR 작업 디렉토리 변경
    > WORKDIR/app 

--도커 허브(docker hub) 이미지 관리
-- hub.docker.com
-- push > docker hub > pull
이미지 저장 명령어
docker login
docker push {ID}/example
docker pull {ID}/example

--배포하기
docker run -d -p 3000:3000 '경로'
    > 컨테이너 실행 = 이미지 pull + 컨테이너 start

--개인실습 Nginx를 이용한 정적 페이지 서버 만들기 
부터시작

# DOCKER 삭제
> curl -O https://raw.githubusercontent.com/docker/toolbox/master/osx/uninstall.sh
> 
> 실행 권한
> 
> chmod +x uninstall.sh
> 
> root 실행
> 
> sudo ./uninstall.sh
------------------------------------------------------------

## DOCKER 실행
> docker run -d -p 80:80 docker/getting-started

## DOCKER 이미지 실행/정지
> docker start/stop [docker ps -a 시 NAMES]

## 실행한 이미지 CLI 접속
> docker exec -it [docker ps 시 CONTAINER ID] /bin/sh