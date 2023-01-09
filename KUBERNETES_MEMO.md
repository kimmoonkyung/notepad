> 큰 기업들은 대규모의 서비스를 운영하고 있기 때문에 최대한 자원을 효율적으로 써야 비용적으로 유리하다.
> 
> 그래서 서버 자원을 효율적으로 쓰기 위해서는 가상화 기술에 대해 관심을 가질 수 밖에 없는데,
> 
> 쿠버네티스를 좀더 잘 이해하려면 가상화기술들에 대한 히스토리를 알 필요가 있다.
> 
> 컨테이너 가상화 기술은 서비스 간에 자원격리를 하는데 OS를 별도로 안 띄워도 된다.
> 
> OS 기동 시간이 없기 떄문에 자동화시에 엄청 빠르고, 자원 효율도 매우 높다.
> 
> 이때부터 도커가 유명세를 탔고, 도커 자체는 하나의 서비스를 컨테이너로 가상화시켜서 배포하는거지, 엄청 많은 서비스 들을 운영 할 때 그걸 일일이 배포하고 운영하는 역할을 해주진 않는다.
> 
> 이런것을 해주는 게 컨테이너 오케스트레이터 라는 개념이다. 여러 컨테이너들을 관리해주는 솔루션이라고 보면 된다.
------------------------

# 실습
```
    vm 설치
        - https://www.virtualbox.org/wiki/Downloads
            - OS X hosts
    CentOS7 iso 파일 다운로드
        - https://img.cs.montana.edu/linux/centos/7.5.1804/isos/x86_64/
            - CentOS-7-x86_64-Minimal-2009.iso
    

```