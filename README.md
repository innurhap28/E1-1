## 1. 실행 환경
 - OS : Darwin Kernel Version 24.6.0
 - SHELL : zsh
 - Docker : 28.5.2
 - Git : 2.53.0

## 2. 수행 체크리스트
 - [x] [터미널 기본 조작 및 폴더 구성](#31-터미널-기본-조작-및-폴더-구성)
 - [x] 권한 변경 실습
 - [x] Docker 설치 및 점검
 - [x] hello-world 실행
 - [x] Dockerfile 빌드 및 실행
 - [x] 포트 매핑 접속 시도
 - [x] 바인드 마운트 반영
 - [x] 볼륨 영속성
 - [x] Git 설정 및 VSCode와 GitHub 연동

## 3. 수행 로그

### 3.1 터미널 기본 조작 및 폴더 구성

```zsh
innuendo3712@c4r6s1 test2 % pwd
/Users/innuendo3712/E1-1/test/test2
```

innuendo3712@c4r6s1 test % cd /
innuendo3712@c4r6s1 / % pwd
/

```zsh
innuendo3712@c4r6s1 test2 % ls -l
total 8
---x------  1 innuendo3712  innuendo3712  14  4  9 23:11 test.sh
```

```zsh
innuendo3712@c4r6s1 test2 % mkdir testing
innuendo3712@c4r6s1 test2 % ls -l
total 8
---x------  1 innuendo3712  innuendo3712  14  4  9 23:11 test.sh
drwxr-xr-x  2 innuendo3712  innuendo3712  64  4  9 23:31 testing
```

innuendo3712@c4r6s1 test2 % ls -al
total 8
drwxr-xr-x  4 innuendo3712  innuendo3712  128  4  9 23:31 .
drwxr-xr-x  6 innuendo3712  innuendo3712  192  4  9 23:35 ..
-rwxrwxrwx  1 innuendo3712  innuendo3712   14  4  9 23:11 test.sh
drwxr-xr-x  2 innuendo3712  innuendo3712   64  4  9 23:31 testing

innuendo3712@c4r6s1 testing % touch hello.txt
innuendo3712@c4r6s1 testing % cat hello.txt
innuendo3712@c4r6s1 testing % vim hello.txt 
innuendo3712@c4r6s1 testing % cat hello.txt
hi

innuendo3712@c4r6s1 testing % mv hello.txt hello2.txt

innuendo3712@c4r6s1 testing % mv hello2.txt ..
innuendo3712@c4r6s1 testing % cd ..
innuendo3712@c4r6s1 test2 % ls
hello2.txt	test.sh		testing

innuendo3712@c4r6s1 test2 % ls
hello2.txt	test.sh
innuendo3712@c4r6s1 test2 % rm test.sh     
innuendo3712@c4r6s1 test2 % ls    
hello2.txt

innuendo3712@c4r6s1 test2 % mkdir testing 
innuendo3712@c4r6s1 test2 % ls
hello2.txt	testing
innuendo3712@c4r6s1 test2 % rmdir testing 
innuendo3712@c4r6s1 test2 % ls
hello2.txt

innuendo3712@c4r6s1 test2 % ls -l
total 8
-rw-r--r--  1 innuendo3712  innuendo3712  3  4  9 23:42 hello2.txt
innuendo3712@c4r6s1 test2 % chmod 600 hello2.txt
innuendo3712@c4r6s1 test2 % ls -l
total 8
-rw-------  1 innuendo3712  innuendo3712  3  4  9 23:42 hello2.txt

innuendo3712@c4r6s1 test2 % mkdir testing
innuendo3712@c4r6s1 test2 % ls -l
total 8
-rw-------  1 innuendo3712  innuendo3712   3  4  9 23:42 hello2.txt
drwxr-xr-x  2 innuendo3712  innuendo3712  64  4  9 23:56 testing
innuendo3712@c4r6s1 test2 % chmod 644 testing
innuendo3712@c4r6s1 test2 % ls -l
total 8
-rw-------  1 innuendo3712  innuendo3712   3  4  9 23:42 hello2.txt
drw-r--r--  2 innuendo3712  innuendo3712  64  4  9 23:56 testing

innuendo3712@c4r6s1 test2 % docker run -it -p 80:80 ubuntu
root@4584165da968:/# 

innuendo3712@c4r6s1 ~ % docker info
Client:
 Version:    28.5.2
 Context:    orbstack
 Debug Mode: false
 Plugins:
  buildx: Docker Buildx (Docker Inc.)
    Version:  v0.29.1
    Path:     /Users/innuendo3712/.docker/cli-plugins/docker-buildx
  compose: Docker Compose (Docker Inc.)
    Version:  v2.40.3
    Path:     /Users/innuendo3712/.docker/cli-plugins/docker-compose

Server:
 Containers: 1
  Running: 1
  Paused: 0
  Stopped: 0
 Images: 1
 Server Version: 28.5.2
 Storage Driver: overlay2
  Backing Filesystem: btrfs
  Supports d_type: true
  Using metacopy: false
  Native Overlay Diff: true
  userxattr: false
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Cgroup Version: 2
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local splunk syslog
 CDI spec directories:
  /etc/cdi
  /var/run/cdi
 Swarm: inactive
 Runtimes: io.containerd.runc.v2 runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 1c4457e00facac03ce1d75f7b6777a7a851e5c41
 runc version: d842d7719497cc3b774fd71620278ac9e17710e0
 init version: de40ad0
 Security Options:
  seccomp
   Profile: builtin
  cgroupns
 Kernel Version: 6.17.8-orbstack-00308-g8f9c941121b1
 Operating System: OrbStack
 OSType: linux
 Architecture: x86_64
 CPUs: 6
 Total Memory: 15.67GiB
 Name: orbstack
 ID: 7a410ac1-63a1-4255-b323-5cbc6c00fc01
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Experimental: false
 Insecure Registries:
  ::1/128
  127.0.0.0/8
 Live Restore Enabled: false
 Product License: Community Engine
 Default Address Pools:
   Base: 192.168.97.0/24, Size: 24
   Base: 192.168.107.0/24, Size: 24
   Base: 192.168.117.0/24, Size: 24
   Base: 192.168.147.0/24, Size: 24
   Base: 192.168.148.0/24, Size: 24
   Base: 192.168.155.0/24, Size: 24
   Base: 192.168.156.0/24, Size: 24
   Base: 192.168.158.0/24, Size: 24
   Base: 192.168.163.0/24, Size: 24
   Base: 192.168.164.0/24, Size: 24
   Base: 192.168.165.0/24, Size: 24
   Base: 192.168.166.0/24, Size: 24
   Base: 192.168.167.0/24, Size: 24
   Base: 192.168.171.0/24, Size: 24
   Base: 192.168.172.0/24, Size: 24
   Base: 192.168.181.0/24, Size: 24
   Base: 192.168.183.0/24, Size: 24
   Base: 192.168.186.0/24, Size: 24
   Base: 192.168.207.0/24, Size: 24
   Base: 192.168.214.0/24, Size: 24
   Base: 192.168.215.0/24, Size: 24
   Base: 192.168.216.0/24, Size: 24
   Base: 192.168.223.0/24, Size: 24
   Base: 192.168.227.0/24, Size: 24
   Base: 192.168.228.0/24, Size: 24
   Base: 192.168.229.0/24, Size: 24
   Base: 192.168.237.0/24, Size: 24
   Base: 192.168.239.0/24, Size: 24
   Base: 192.168.242.0/24, Size: 24
   Base: 192.168.247.0/24, Size: 24
   Base: fd07:b51a:cc66:d000::/56, Size: 64

WARNING: DOCKER_INSECURE_NO_IPTABLES_RAW is set

innuendo3712@c4r6s1 ~ % docker images
REPOSITORY   TAG       IMAGE ID       CREATED      SIZE
ubuntu       latest    b28307c40a80   6 days ago   78.1MB

innuendo3712@c4r6s1 ~ % docker ps
CONTAINER ID   IMAGE     COMMAND       CREATED          STATUS         PORTS                                 NAMES
4584165da968   ubuntu    "/bin/bash"   14 minutes ago   Up 2 minutes   0.0.0.0:80->80/tcp, [::]:80->80/tcp   lucid_chaplygin

innuendo3712@c4r6s1 ~ % docker ps -a
CONTAINER ID   IMAGE     COMMAND       CREATED          STATUS         PORTS                                 NAMES
4584165da968   ubuntu    "/bin/bash"   17 minutes ago   Up 5 minutes   0.0.0.0:80->80/tcp, [::]:80->80/tcp   lucid_chaplygin

innuendo3712@c4r6s1 ~ % docker logs lucid_chaplygin
root@4584165da968:/# sudo mkdir 1
bash: sudo: command not found
root@4584165da968:/# docker --version
bash: docker: command not found
root@4584165da968:/#

innuendo3712@c4r6s1 ~ % docker logs -f lucid_chaplygin
root@4584165da968:/# sudo mkdir 1
bash: sudo: command not found
root@4584165da968:/# docker --version
bash: docker: command not found
root@4584165da968:/#

innuendo3712@c4r6s1 ~ % docker logs --tail 1 lucid_chaplygin 
root@4584165da968:/# 

innuendo3712@c4r6s1 ~ % docker stats --no-stream
CONTAINER ID   NAME              CPU %     MEM USAGE / LIMIT    MEM %     NET I/O         BLOCK I/O     PIDS
4584165da968   lucid_chaplygin   0.00%     5.32MiB / 15.67GiB   0.03%     1.13kB / 126B   29.1MB / 0B   5


innuendo3712@c4r6s1 E1-1 % mkdir docker-project 
innuendo3712@c4r6s1 E1-1 % cd docker-project   
innuendo3712@c4r6s1 docker-project % vim app/index.html
innuendo3712@c4r6s1 docker-project % ls 
innuendo3712@c4r6s1 docker-project % mkdir app
innuendo3712@c4r6s1 docker-project % vim app/index.html
innuendo3712@c4r6s1 docker-project % cd app 
innuendo3712@c4r6s1 app % ls
index.html
innuendo3712@c4r6s1 app % cat index.html 
<!DOCTYPE html>
<html>
<head>
        <title>Docker Project</title>
</head>
<body>
        <h1>Hello Docker!</h1>
        <p>Hello Docker!</p>
</body>
</html>
innuendo3712@c4r6s1 app % cd ..
innuendo3712@c4r6s1 docker-project % vim Dockerfile
innuendo3712@c4r6s1 docker-project % cat Dockerfile
FROM nginx:ubuntu
COPY app/index.html /usr/share/nginx/html/index.html

innuendo3712@c4r6s1 docker-project % docker build -t my-web .
[+] Building 6.5s (7/7) FINISHED                                                                                      docker:orbstack
 => [internal] load build definition from Dockerfile                                                                             0.1s
 => => transferring dockerfile: 109B                                                                                             0.0s
 => [internal] load metadata for docker.io/library/nginx:alpine                                                                  1.9s
 => [internal] load .dockerignore                                                                                                0.1s
 => => transferring context: 2B                                                                                                  0.0s
 => [internal] load build context                                                                                                0.2s
 => => transferring context: 229B                                                                                                0.0s
 => [1/2] FROM docker.io/library/nginx:alpine@sha256:645eda1c2477aaa9b879f73909b9222c6f19798dd45be6706268d82a661c6e6d            3.6s
 => => resolve docker.io/library/nginx:alpine@sha256:645eda1c2477aaa9b879f73909b9222c6f19798dd45be6706268d82a661c6e6d            0.2s
 => => sha256:c1263cc56873d66f381fd07149aa0dc7244dd7c941334cd18473c46509f08465 2.50kB / 2.50kB                                   0.0s
 => => sha256:589002ba0eaed121a1dbf42f6648f29e5be55d5c8a6ee0f8eaa0285cc21ac153 3.86MB / 3.86MB                                   0.5s
 => => sha256:645eda1c2477aaa9b879f73909b9222c6f19798dd45be6706268d82a661c6e6d 10.33kB / 10.33kB                                 0.0s
 => => sha256:5bd7bd52e5bcab15a093466b90e37472b0d0c0081052522afb8924cbdaf15f56 12.32kB / 12.32kB                                 0.0s
 => => sha256:f03becc8ac15611cfcc421c977a5ba4d65456093570788523a4ba557689aa7f7 1.87MB / 1.87MB                                   0.8s
 => => sha256:15e759724ff67f262e38bb7c070af9d0b84f959f9b37fa966f68bf2f881a4b62 627B / 627B                                       0.9s
 => => extracting sha256:589002ba0eaed121a1dbf42f6648f29e5be55d5c8a6ee0f8eaa0285cc21ac153                                        0.1s
 => => sha256:ff9f59a6a62e9e9f29d7a84fb18865b45664d3f0d061eff7548bd61746dd101c 957B / 957B                                       1.0s
 => => extracting sha256:f03becc8ac15611cfcc421c977a5ba4d65456093570788523a4ba557689aa7f7                                        0.1s
 => => sha256:a71873b303e8d75170b7ced2725b01b3ae15ad76f0d4eef16a49335821b6a0ef 404B / 404B                                       1.2s
 => => sha256:34dfdd2ef1f920d0054dde2fc09ddc83ff8e71d05fadb79e2cab6e6234596f0a 1.21kB / 1.21kB                                   1.3s
 => => extracting sha256:15e759724ff67f262e38bb7c070af9d0b84f959f9b37fa966f68bf2f881a4b62                                        0.0s
 => => sha256:c8a2fa3a88d244a3f32dcbc9c1f7649c662661a28c624198ada43aa0b7598e7f 1.40kB / 1.40kB                                   1.5s
 => => extracting sha256:ff9f59a6a62e9e9f29d7a84fb18865b45664d3f0d061eff7548bd61746dd101c                                        0.0s
 => => extracting sha256:a71873b303e8d75170b7ced2725b01b3ae15ad76f0d4eef16a49335821b6a0ef                                        0.0s
 => => sha256:1165b869c51a1a0747d78cec8fab96c30156a979e51ecf2f91aa792e557d94a4 20.25MB / 20.25MB                                 2.0s
 => => extracting sha256:34dfdd2ef1f920d0054dde2fc09ddc83ff8e71d05fadb79e2cab6e6234596f0a                                        0.0s
 => => extracting sha256:c8a2fa3a88d244a3f32dcbc9c1f7649c662661a28c624198ada43aa0b7598e7f                                        0.0s
 => => extracting sha256:1165b869c51a1a0747d78cec8fab96c30156a979e51ecf2f91aa792e557d94a4                                        0.4s
 => [2/2] COPY app/index.html /usr/share/nginx/html/index.html                                                                   0.3s
 => exporting to image                                                                                                           0.2s
 => => exporting layers                                                                                                          0.1s
 => => writing image sha256:bb756637613294f2bd8c4cc7a0b6726ee007ee753c20feca54b0dc669027d22f                                     0.0s
 => => naming to docker.io/library/my-web                                                                                        0.0s


 innuendo3712@c4r6s1 docker-project % docker run -d -p 8080:80 my-web
168cecf8ad8be6d21fc5a7b5e1e6bc60d5d71dcf128317e90b37a09628aaec2c

innuendo3712@c4r6s1 docker-project % docker run -v my-volume:/data ubuntu bash -c "echo 'persistent data' > /data/test.txt"

innuendo3712@c4r6s1 docker-project % docker run -v my-volume:/data ubuntu bash -c "cat /data/test.txt"
persistent data


innuendo3712@c4r6s1 E1-1 % git config --list          
credential.helper=osxkeychain
user.name=innurhap28
user.email=kmugi118@gmail.com
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
core.ignorecase=true
core.precomposeunicode=true
remote.origin.url=https://github.com/innurhap28/E1-1.git
remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
branch.main.remote=origin
branch.main.merge=refs/heads/main
branch.main.vscode-merge-base=origin/main

### 트러블슈팅

innuendo3712@c4r6s1 docker-project % docker build -t my-web .
[+] Building 1.9s (2/2) FINISHED                                                                                      docker:orbstack
 => [internal] load build definition from Dockerfile                                                                             0.2s
 => => transferring dockerfile: 109B                                                                                             0.0s
 => ERROR [internal] load metadata for docker.io/library/nginx:ubuntu                                                            1.4s
------
 > [internal] load metadata for docker.io/library/nginx:ubuntu:
------
Dockerfile:1
--------------------
   1 | >>> FROM nginx:ubuntu
   2 |     COPY app/index.html /usr/share/nginx/html/index.html
   3 |     
--------------------
ERROR: failed to build: failed to solve: nginx:ubuntu: failed to resolve source metadata for docker.io/library/nginx:ubuntu: docker.io/library/nginx:ubuntu: not found
innuendo3712@c4r6s1 docker-project % vim Dockerfile 
innuendo3712@c4r6s1 docker-project % cat Dockerfile          
FROM nginx:alpine
COPY app/index.html /usr/share/nginx/html/index.html