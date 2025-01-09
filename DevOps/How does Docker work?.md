# 도커의 작동 방식
![alt text](https://github.com/ByteByteGoHq/system-design-101/blob/main/images/docker.jpg?raw=true)
> 우리가 docker build, docker pull, docker run을 실행시켰을 때의 동장 방식 및 도커의 아키텍쳐를 설명한 다이어그램

## Docker client
도커 클라이언트는 도커 데몬과 통신하여 사용자의 명령어를 전달해준다.

## Docker host
도커 데몬은 도커 API 요청을 받아 이미지, 컨테이너, 네트워크 그리고 볼륨 같은 도커 오브젝트 들을 관리한다.

![alt text](https://github.com/kjr2020/eddie-storage/blob/main/images/dockerd.jpg?raw=true)

### 도커 데몬
 - 도커 데몬은 백그라운드에서 실행되며, 서버-클라이언트 아키텍처로 설계되어 있다.
 - RESTful API를 통해 클라이언트(Docker CLI, GUI 등)와 상호 작용을 한다.(docker run, docker pull 등)

## Docker registry
![alt text](https://github.com/kjr2020/eddie-storage/blob/main/images/dockerhub.png?raw=true)
<br>
도커 레지스트리는 도커 이미지를 저장하는 역할을 하며, 도커 허브에 저장된 이미지는 누구나 사용 가능하다.
<br>
Docker Hub, GitHub Container Registry(GHCR), Google Artifact Registry, Amazon Elastic Container Registry(ECR) 등이 있다.

## docker run 명령어의 작동 방식

1. 도커가 도커 레지스트리에서 이미지를 가져온다.
2. 가져온 이미지를 기반으로 새로운 컨테이너를 만든다.
3. 도커가 컨테이너에게 파일시스템의 읽기-쓰기를 허용한다.
4. 컨테이너가 기본 네트워크에 연결할 수 있도록 네트워크 인터페이스를 만들어준다.
5. 컨테이너를 시작한다.

## docker build 명령어의 작동 방식

1. 빌드 컨텍스트를 도커 데몬으로 전송한다. (도커 컨텍스트에는 Dockerfile과 이미지 빌드에 필요한 모든 파일이 포함됨)
2. 도커 데몬이 Dockerfile의 각 명령을 실행한다.(도커는 명령을 실행할 때마다 새로운 이미지 layer를 생성하며, 이는 캐시되어 재사용이 가능하다.)
3. Dockerfile의 모든 명령이 실행되면 최종적으로 하나의 이미지를 생성하게된다.