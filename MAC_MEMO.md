--작업관리자
opt + cmd + esc

--스샷
shift + cmd + 3
--일부 스샷
shift + cmd + 4

--열려 있는 프로그램끼리의 전환
" cmd + ` "

--데스크탑 추가
트랙패드 손가락 네개 위로 
--데스크탑 전환
ctrl + 좌우 방향키
트랙패드 손가락 세개 좌우

--크롬 개발자 도구
cmd + opt + i

# jenkin 설치
> brew install jenkins-lts
## jenkins 시작/종료/재시작
> brew services start/stop/restart jenkins-lts 
## local 비밀 번호
> /Users/kimmoonkyung/.jenkins/secrets/initialAdminPassword

## jenkins docker에 설치
> docker run -itd --name jenkins -p 9999:8080 jenkins/jenkins:lts
```
run : 이미지를 실행
-itd 옵션: interacitve terminal + detach(background)
--name : 이미지 이름 지정
-p: <hostport>:<docker container port>
jenkins/jenkins:lts: docker hub이미지 저장소:버전

    localhost:9999 접속
```
### docker에 설치한 젠킨스 비밀번호 확인
> docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword