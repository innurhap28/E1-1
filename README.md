## 1. 실행 환경

| 항목 | 버전 |
|------|------|
| OS | Darwin Kernel Version 24.6.0 |
| SHELL | zsh |
| Docker | 28.5.2 |
| Git | 2.53.0 |

---

## 2. 수행 체크리스트

- [x] [터미널 기본 조작 및 폴더 구성](#31-터미널-기본-조작-및-폴더-구성)
- [x] [권한 변경 실습](#32-권한-변경-실습)
- [x] [Docker 설치 및 점검](#33-docker-설치-및-점검)
- [x] [hello-world 실행](#34-hello-world-실행)
- [x] [Dockerfile 빌드 및 실행](#35-dockerfile-빌드-및-실행)
- [x] [포트 매핑 접속 시도](#36-포트-매핑-접속-시도)
- [x] [바인드 마운트 반영](#37-바인드-마운트-반영)
- [x] [볼륨 영속성](#38-볼륨-영속성)
- [x] [Git 설정 및 VSCode와 GitHub 연동](#39-git-설정-및-vscode와-github-연동)

---

## 3. 수행 로그

### 3.1 터미널 기본 조작 및 폴더 구성

현재 경로 확인 및 루트 디렉토리 이동:

```zsh
innuendo3712@c4r6s1 test2 % pwd
/Users/innuendo3712/E1-1/test/test2

innuendo3712@c4r6s1 test % cd /
innuendo3712@c4r6s1 / % pwd
/
```

파일 목록 확인:

```zsh
innuendo3712@c4r6s1 test2 % ls -l
total 8
---x------  1 innuendo3712  innuendo3712  14  4  9 23:11 test.sh
```

디렉토리 생성 및 확인:

```zsh
innuendo3712@c4r6s1 test2 % mkdir testing
innuendo3712@c4r6s1 test2 % ls -l
total 8
---x------  1 innuendo3712  innuendo3712  14  4  9 23:11 test.sh
drwxr-xr-x  2 innuendo3712  innuendo3712  64  4  9 23:31 testing
```

숨김 파일 포함 전체 목록 확인:

```zsh
innuendo3712@c4r6s1 test2 % ls -al
total 8
drwxr-xr-x  4 innuendo3712  innuendo3712  128  4  9 23:31 .
drwxr-xr-x  6 innuendo3712  innuendo3712  192  4  9 23:35 ..
-rwxrwxrwx  1 innuendo3712  innuendo3712   14  4  9 23:11 test.sh
drwxr-xr-x  2 innuendo3712  innuendo3712   64  4  9 23:31 testing
```

파일 생성, 편집, 이동, 삭제:

```zsh
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
```

파일 및 디렉토리 삭제:

```zsh
innuendo3712@c4r6s1 test2 % rm test.sh
innuendo3712@c4r6s1 test2 % ls
hello2.txt

innuendo3712@c4r6s1 test2 % mkdir testing
innuendo3712@c4r6s1 test2 % rmdir testing
innuendo3712@c4r6s1 test2 % ls
hello2.txt
```

---

### 3.2 권한 변경 실습

파일 권한 변경 (644 → 600):

```zsh
innuendo3712@c4r6s1 test2 % ls -l
total 8
-rw-r--r--  1 innuendo3712  innuendo3712  3  4  9 23:42 hello2.txt

innuendo3712@c4r6s1 test2 % chmod 600 hello2.txt
innuendo3712@c4r6s1 test2 % ls -l
total 8
-rw-------  1 innuendo3712  innuendo3712  3  4  9 23:42 hello2.txt
```

디렉토리 권한 변경 (755 → 644):

```zsh
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
```

---

### 3.3 Docker 설치 및 점검

Docker 시스템 정보 확인:

```zsh
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
 ...
```

이미지 및 컨테이너 목록 확인:

```zsh
innuendo3712@c4r6s1 ~ % docker images
REPOSITORY   TAG       IMAGE ID       CREATED      SIZE
ubuntu       latest    b28307c40a80   6 days ago   78.1MB

innuendo3712@c4r6s1 ~ % docker ps
CONTAINER ID   IMAGE     COMMAND       CREATED          STATUS         PORTS                                 NAMES
4584165da968   ubuntu    "/bin/bash"   14 minutes ago   Up 2 minutes   0.0.0.0:80->80/tcp, [::]:80->80/tcp   lucid_chaplygin

innuendo3712@c4r6s1 ~ % docker ps -a
CONTAINER ID   IMAGE     COMMAND       CREATED          STATUS         PORTS                                 NAMES
4584165da968   ubuntu    "/bin/bash"   17 minutes ago   Up 5 minutes   0.0.0.0:80->80/tcp, [::]:80->80/tcp   lucid_chaplygin
```

---

### 3.4 hello-world 실행

Ubuntu 컨테이너 실행 (포트 매핑 포함):

```zsh
innuendo3712@c4r6s1 test2 % docker run -it -p 80:80 ubuntu
root@4584165da968:/#
```

컨테이너 로그 확인:

```zsh
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
```

컨테이너 리소스 사용량 확인:

```zsh
innuendo3712@c4r6s1 ~ % docker stats --no-stream
CONTAINER ID   NAME              CPU %     MEM USAGE / LIMIT    MEM %     NET I/O         BLOCK I/O     PIDS
4584165da968   lucid_chaplygin   0.00%     5.32MiB / 15.67GiB   0.03%     1.13kB / 126B   29.1MB / 0B   5
```

---

### 3.5 Dockerfile 빌드 및 실행

프로젝트 디렉토리 구성 및 `index.html` 작성:

```zsh
innuendo3712@c4r6s1 E1-1 % mkdir docker-project
innuendo3712@c4r6s1 E1-1 % cd docker-project
innuendo3712@c4r6s1 docker-project % mkdir app
innuendo3712@c4r6s1 docker-project % vim app/index.html
innuendo3712@c4r6s1 app % cat index.html
```

```html
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
```

`Dockerfile` 작성:

```zsh
innuendo3712@c4r6s1 docker-project % vim Dockerfile
innuendo3712@c4r6s1 docker-project % cat Dockerfile
```

```dockerfile
FROM nginx:alpine
COPY app/index.html /usr/share/nginx/html/index.html
```

이미지 빌드:

```zsh
innuendo3712@c4r6s1 docker-project % docker build -t my-web .
[+] Building 6.5s (7/7) FINISHED                             docker:orbstack
 => [internal] load build definition from Dockerfile                    0.1s
 => [internal] load metadata for docker.io/library/nginx:alpine         1.9s
 => [internal] load build context                                       0.2s
 => [1/2] FROM docker.io/library/nginx:alpine@sha256:645eda1c...        3.6s
 => [2/2] COPY app/index.html /usr/share/nginx/html/index.html          0.3s
 => exporting to image                                                  0.2s
 => => naming to docker.io/library/my-web                               0.0s
```

---

### 3.6 포트 매핑 접속 시도

컨테이너를 백그라운드로 실행하고 포트 매핑:

```zsh
innuendo3712@c4r6s1 docker-project % docker run -d -p 8080:80 my-web
168cecf8ad8be6d21fc5a7b5e1e6bc60d5d71dcf128317e90b37a09628aaec2c
```

> 브라우저에서 `http://localhost:8080` 접속 시 "Hello Docker!" 페이지 확인

---

### 3.7 바인드 마운트 반영

> 바인드 마운트는 호스트 디렉토리를 컨테이너에 실시간으로 연결하는 방식입니다.

```zsh
docker run -d -p 8080:80 -v $(pwd)/app:/usr/share/nginx/html my-web
```

---

### 3.8 볼륨 영속성

볼륨에 데이터 쓰기:

```zsh
innuendo3712@c4r6s1 docker-project % docker run -v my-volume:/data ubuntu \
  bash -c "echo 'persistent data' > /data/test.txt"
```

볼륨 데이터 재확인 (컨테이너 재시작 후에도 데이터 유지):

```zsh
innuendo3712@c4r6s1 docker-project % docker run -v my-volume:/data ubuntu \
  bash -c "cat /data/test.txt"
persistent data
```

---

### 3.9 Git 설정 및 VSCode와 GitHub 연동

Git 설정 확인:

```zsh
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
```

---

## 4. 트러블슈팅

### `nginx:ubuntu` 태그 없음 오류

**문제:** Dockerfile에 존재하지 않는 `nginx:ubuntu` 태그를 지정하여 빌드 실패

```zsh
innuendo3712@c4r6s1 docker-project % docker build -t my-web .
 => ERROR [internal] load metadata for docker.io/library/nginx:ubuntu
------
ERROR: failed to build: failed to solve: nginx:ubuntu: failed to resolve source metadata \
  for docker.io/library/nginx:ubuntu: docker.io/library/nginx:ubuntu: not found
```

**해결:** `Dockerfile`에서 태그를 `nginx:ubuntu` → `nginx:alpine`으로 수정

```dockerfile
# 수정 전
FROM nginx:ubuntu

# 수정 후
FROM nginx:alpine
COPY app/index.html /usr/share/nginx/html/index.html