# docker-study

## env
    ec2 ubuntu

## install
  #### 도커와 관련된 패키지들을 제거
    for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
    
  #### Ubuntu 리눅스 시스템에 도커 설치를 설치하기 위한 선행 명령어
    sudo apt-get update
    sudo apt-get install ca-certificates curl gnupg
    sudo install -m 0755 -d /etc/apt/keyrings
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    sudo chmod a+r /etc/apt/keyrings/docker.gpg
    
    echo \
      "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
      "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
      sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
      
    sudo apt-get update

  #### 도커 최신 버전 설
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin


## COMMANDS
  #### 컨테이너 실행(이미지 없을 경우 이미지 다운로드 후 컨테이너 실행, 태그가 없는 경우 디폴트로 latest로 다운로드)
    docker run {이미지 이름}    

  #### 컨테이너 삭제
    docker rm {컨테이너 이름}

  #### 이미지 삭제
     docker rmi {이미지 이름}

  #### 다운로드된 이미지 보기
     docker images

  #### 이미지 다운로드 컨테이너 실행x
    docker pull {이미지 이름}

  #### 컨테이너 이름 지정
    docker run --name {컨테이너 이름} {이미지 이름} -> 포트를 열어주지 않아 호스트에서 접속불가
  
  #### 컨네이터의 포트를 호스트의 포트와 연결
     docker run --name {컨테이너 이름} -p {호스트 포트}:{컨테이너 포트} {이미지 이름}

  #### mysql을 백그라운드 실행
     docker run --name mysql -p3308:3306 -e MYSQL_ROOT_PASSWORD={} -d mysql
  
  #### 컨테이너 실행
     docker start {tag or pid}

  #### 컨테이너 정지
     docker stop {tag or pid}

  #### 컨테이너 로그
     docker logs {tag or pid}

  #### 실행중인 컨테어니에 접속
     docker attach {pid or name}

  #### 도커 볼륨
     // 컨테이너를 삭제시 해당 컨테이너에 저장되있던 데이터도 같이 삭제되기 때문에 볼륨 옵션(-v)을 주어 볼륨 컨테이너를 생성하여 저정한 호스트의 디렉터리와 공유한다.
     // (/var/lib/mysql 디렉터리는 MySQL이 데이터베이스의 데이터를 저장하는 기본 디렉터리이다.)
     docker run --name my-mysql -p3307:3306 -e MYSQL_ROOT_PASSWORD=rlatnehd@123 -v C:\\tmp\\mysql:/var/lib/mysql -d mysql:latest

  #### Dockerfile로 mysql 이미지 만들기
     docker build -t {이미지 이름} -f 도커 파일 경로(보통 root경로에 있음)
     ex) docker build -t dockerfile-mysql -f ./docker/Dockerfile .

  #### 컨테이너를 실행후 컨테이너에 접속
    docker run -i -t {이미지 이름} {실행 명령어}

  #### 컨테이너의 자원 변경
     docker update {변경할 자원 제한} {컨테이너 이름}

  #### 


