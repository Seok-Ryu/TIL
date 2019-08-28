
# 기본 명령어
 - docker images
 - docker run {repositoryName}
 - docker ps
 - docker ps -a (종료된 내용 포함)
 - docker build -t {image-name}:{tag-version} .
   - `t`는 태그옵션
   - docker build -t node-app:0.1 .
   - 현 디렉토리에 node-app 이미지를 생성 태그는 0.1
 - docker run -p {host-port}:{container-port} --name {name} -d {image-name}:{tag}
   - `p`는 포트 옵션. 호스트포트:컨테이너포트
   - `name` 편의를 위한 네이밍 옵션
   - `d`는 백그라운드 옵션
   - docker run -p 4000:80 --name my-app node-app:0.1
 - docker stop {name}
 - docker rm {name}
 - docker logs -f {container-id} 
   - `f` 실행중 상태로 출력
 - docker exec -it {container_id} bash
   - container bash 에 접근
   - https://docs.docker.com/engine/reference/commandline/exec/
 - docker inspect {container_id}
   - container's metadata 
   - https://docs.docker.com/engine/reference/commandline/inspect/#examples
 - docker push {url/image-name:tag}
   - image push
 - docker tag {image-name:tag} {new-image-name:new-tag}
 - docker rmi {image-name}
 - docker pull {url}
 
  
 
 
