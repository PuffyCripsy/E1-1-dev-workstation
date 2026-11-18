README

# E1-1 개발 워크스테이션 구축

> Codyssey E1-1 미션 — Linux CLI · Docker · Git/GitHub 실습 기록
> 
> 
> 실습 1~13 및 Docker Compose 보너스 실습의 수행 절차, 검증 결과 및 증빙 자료
> 

## 1. 프로젝트 개요

Windows의 WSL2 Ubuntu 환경에서 Linux 기본 명령어, 파일 권한, Docker 컨테이너, NGINX 웹 서버, 포트 매핑, 바인드 마운트, Docker 볼륨, Git/GitHub 연동과 Docker Compose 기반 NGINX 실행을 실습하였다. 저장소에 Dockerfile과 웹페이지 소스를 포함하고, 실행 절차와 검증 결과를 문서화하였다.

**관련 자료**: 미션 요구사항 · 스크린샷 폴더

## 2. 개발 환경

| 항목 | 환경 |
| --- | --- |
| 운영체제 | Windows, WSL2 Ubuntu |
| 터미널/셸 | Ubuntu Terminal / Bash |
| 에디터 | Visual Studio Code |
| Docker | Docker Desktop 29.9.2 |
| Git | 2.55 (기존 GitHub README 기록 기준) |
| GitHub 저장소 | PuffyCripsy/E1-1-dev-workstation |
| 실습 웹 서버 | NGINX (`nginx:alpine`) |
| Docker Compose | v5.3.1 (Windows PowerShell에서 확인) |

실습 환경은 공용 컴퓨터를 포함하며, 사용자명·호스트명·Docker 이미지 ID·경로·출력 시각은 실행 환경에 따라 달라질 수 있다.

### 수행 체크리스트

- [x]  실습 1~5: Linux 기본 명령어, 파일·폴더 조작, 권한 변경
- [x]  실습 6~8: Docker 설치/엔진 점검, hello-world, Ubuntu 컨테이너, 운영 명령
- [x]  실습 9: Dockerfile 직접 작성 및 이미지 빌드
- [x]  실습 10: 호스트 8080 → 컨테이너 80 포트 매핑, 브라우저 접속
- [x]  실습 11: 바인드 마운트 수정 전·후 비교
- [x]  실습 12: 컨테이너 삭제 전·후 볼륨 데이터 유지 확인
- [x]  실습 13: Git 설정, VS Code에서 Git 저장소 확인, GitHub 인증 및 Push
- [x]  보너스 과제: Docker Compose 설정 파일 작성, NGINX 실행, 상태 및 브라우저 접속 확인

## 3. Linux 기본 명령어 실습 (실습 1~5)

### 실습 1. 디렉터리와 빈 파일 생성

```bash
cd ~
mkdir practice
cd practice
touch hello.txt
ls -l
```

`cd`는 이동, `mkdir`는 디렉터리 생성, `touch`는 빈 파일 생성, `ls -l`은 상세 목록을 확인하는 명령어이다. `hello.txt` 파일 생성과 목록 표시를 확인하였다.

### 실습 2. 파일 내용 쓰기·읽기

```bash
echo "Hello Linux" > hello.txt
cat hello.txt
```

확인한 내용:

```
Hello Linux
```

`>`는 기존 파일 내용을 덮어쓰는 출력 리다이렉션이고, `cat`은 파일 내용을 표시한다.

### 실습 3. 복사·이름 변경·이동·삭제

```bash
cp hello.txt hello_copy.txt
mv hello_copy.txt hello_backup.txt
mkdir backup
mv hello_backup.txt backup/
ls -l backup/
rm backup/hello_backup.txt
ls -l backup/
```

복사 후 원본 파일이 유지되고, 파일 이름 변경·폴더 이동·삭제가 실행되는 과정을 확인하였다. `rm`은 일반적으로 휴지통을 거치지 않으므로 주의해야 한다.

### 실습 4. 파일과 디렉터리 권한 변경

```bash
cd ~/practice
ls -ld hello.txt backup
chmod 600 hello.txt
ls -l hello.txt
chmod 700 backup
ls -ld backup
```

| 대상 | 변경 전 예시 | 변경 후 확인 |
| --- | --- | --- |
| 파일 `hello.txt` | `-rw-r--r--` (644) | `-rw-------` (600) |
| 폴더 `backup` | `drwxr-xr-x` (755) | `drwx------` (700) |

`r=4`(읽기), `w=2`(쓰기), `x=1`(실행·디렉터리 접근)로 표현한다. `600`은 파일 소유자만 읽기·쓰기, `700`은 폴더 소유자만 읽기·쓰기·접근할 수 있는 권한이다. 디렉터리 자체의 권한은 `ls -ld`로 확인하였다.

### 실습 5. 경로 및 숨김 항목 확인

```bash
pwd
ls -la
```

`pwd`는 현재 디렉터리의 절대 경로를, `ls -la`는 숨김 항목까지 포함한 상세 목록을 출력한다. `~`는 홈 디렉터리, `.`는 현재 폴더, `..`는 상위 폴더를 의미한다.

**증빙 자료:** Linux 실습 기록

## 4. Docker 기본 실습 (실습 6~8)

### 실습 6. Docker 설치·엔진 점검과 hello-world

```bash
docker --version
docker info
docker run hello-world
```

Docker Desktop과 WSL2 연동을 통해 Docker 명령을 실행하였다. Docker Desktop 29.9.2 환경에서 `hello-world` 컨테이너의 정상 실행을 확인하였다. `docker --version`은 CLI 버전을, `docker info`는 엔진 정보를 확인한다.

### 실습 7. Ubuntu 컨테이너 진입과 실행 방식

```bash
docker run -it ubuntu bash
# 컨테이너 내부에서 ls, echo 등 실행
exit
```

- `it`는 대화형 터미널을 제공하고, `exit`는 컨테이너 셸을 종료한다. 백그라운드 컨테이너에는 `docker exec`로 추가 명령을 실행할 수 있다. `docker run`은 새 컨테이너를 만들고, `docker start`는 기존 컨테이너를 재시작한다.

### 실습 8. 이미지·컨테이너 운영 명령

```bash
docker images
docker ps
docker ps -a
docker logs <컨테이너명>
docker stats --no-stream
docker stop <컨테이너명>
docker rm <컨테이너명>
```

`images`는 이미지 목록, `ps -a`는 종료된 컨테이너까지 포함한 목록, `logs`는 실행 로그, `stats`는 CPU·메모리 등 자원 사용량을 보여준다. `<컨테이너명>`은 명령어의 매개변수 위치를 나타낸다.

**증빙 자료:** screenshots 폴더

## 5. Dockerfile 및 웹 서버 (실습 9~10)

### 실습 9. NGINX 커스텀 이미지 빌드

실제로 작성하여 GitHub에 올린 Dockerfile:

```docker
FROM nginx:alpine
COPY html/ /usr/share/nginx/html/
EXPOSE 80
```

- `FROM`: 공식 NGINX 기반 이미지 선택
- `COPY`: 직접 만든 HTML을 NGINX의 기본 문서 경로로 복사
- `EXPOSE`: 컨테이너의 HTTP 80 포트를 문서화 (`p`와는 다름)

```bash
cd ~/practice/custom-nginx
docker build -t my-custom-nginx:1.0 .
```

`my-custom-nginx:1.0` 이미지 빌드에 성공하였다. **이미지**는 실행 환경을 담은 템플릿이고, **컨테이너**는 그 이미지를 실제로 실행한 인스턴스이다.

### 실습 10. 포트 매핑 및 브라우저 접속

```bash
docker run -d -p 8080:80 --name my-web-8080 my-custom-nginx:1.0
```

브라우저에서 `http://localhost:8080`에 접속하여 웹페이지가 표시되는 것을 확인하였다. `-p 8080:80`은 **호스트 8080 → 컨테이너 80** 연결이다. 주소창과 페이지 내용이 함께 보이는 스크린샷을 증거로 사용한다.

**증빙 자료:** 포트 매핑 접속 화면

## 6. 스토리지 연결 및 데이터 영속성 (실습 11~12)

### 실습 11. 바인드 마운트: 파일 수정 즉시 반영

```bash
cd ~/practice/custom-nginx
docker run -d -p 8082:80 -v "$(pwd)/html:/usr/share/nginx/html" --name web-mount my-custom-nginx:1.0
curl -s http://localhost:8082 | grep "구동"
sed -i 's/정상 구동 중입니다!/바인드 마운트로 실시간 반영 성공!/g' html/index.html
curl -s http://localhost:8082 | grep "바인드 마운트"
docker stop web-mount && docker rm web-mount
```

**변경 전 확인:**

```html
<p>Docker 커스텀 이미지로 정상 구동 중입니다!</p>
```

**변경 후 확인:**

```html
<p>Docker 커스텀 이미지로 바인드 마운트로 실시간 반영 성공!</p>
```

호스트의 `html/index.html`을 수정하자 이미지 재빌드나 컨테이너 재시작 없이 `curl` 응답이 변경되었다. 바인드 마운트는 호스트 폴더를 컨테이너 경로에 직접 연결하는 방식이다.

**증빙 자료:** 바인드 마운트 실습 스크린샷

### 실습 12. Docker 볼륨: 컨테이너 삭제 후에도 데이터 유지

```bash
docker volume create my-workstation-data
docker run -d --name vol-writer -v my-workstation-data:/data ubuntu sleep infinity
docker exec vol-writer bash -c "echo 'Hello Docker Volume' > /data/report.txt"
docker exec vol-writer cat /data/report.txt
# Hello Docker Volume

docker rm -f vol-writer
docker run -d --name vol-reader -v my-workstation-data:/data ubuntu sleep infinity
docker exec vol-reader cat /data/report.txt
# Hello Docker Volume

docker rm -f vol-reader
docker volume rm my-workstation-data
```

PC를 재시작한 뒤에는 필요에 따라 `docker start vol-writer`로 기존 컨테이너를 다시 시작하였다. 첫 번째 컨테이너를 삭제하고 두 번째 컨테이너에서 **동일한 `Hello Docker Volume` 출력**을 확인하였다. 이는 Docker 볼륨이 컨테이너 삭제와 별개로 데이터를 유지함을 보여준다. 검증 후 테스트 컨테이너와 볼륨을 정리하였다.

| 비교 | 바인드 마운트 | Docker 볼륨 |
| --- | --- | --- |
| 저장 위치 | 지정한 호스트 폴더 | Docker가 관리하는 저장 영역 |
| 주요 활용 | 개발 소스 즉시 반영 | 컨테이너 삭제 후에도 데이터 유지 |

**증빙 자료:** 볼륨 영속성 실습 스크린샷

## 7. Git 설정 및 GitHub/VS Code 연동 (실습 13)

### 실제 설정 및 확인

```bash
git --version
# git version 2.53

git config --global user.name "Cripsy"
git config --global user.email "jfyouni@naver.com"
git config --global init.defaultBranch main
git config --list
# user.name=Cripsy
# user.email=jfyouni@naver.com
# init.defaultbranch=main

cd ~/E1-1-dev-workstation
git remote -v
# origin https://github.com/PuffyCripsy/E1-1-dev-workstation.git (fetch)
# origin https://github.com/PuffyCripsy/E1-1-dev-workstation.git (push)

git status
# On branch main
# Your branch is up to date with 'origin/main'.
# nothing to commit, working tree clean

code .
```

VS Code에서 저장소, `main` 브랜치, 소스 제어의 커밋 기록을 확인하였다. GitHub CLI(`gh`)를 설치하고 브라우저 인증으로 `PuffyCripsy` 계정 로그인을 완료하였다. WSL에서 브라우저가 자동 실행되지 않아 Windows 브라우저에서 `https://github.com/login/device`에 직접 접속하였다. 인증 코드는 기록하지 않았다.

### Docker 실습 파일을 GitHub에 업로드

```bash
cp -r ~/practice/custom-nginx ~/E1-1-dev-workstation/
cd ~/E1-1-dev-workstation
git add custom-nginx/
git commit -m "Add Docker custom nginx practice files"
git push origin main
```

커밋 결과:

```
[main 154978f] Add Docker custom nginx practice files
 2 files changed, 14 insertions(+)
 create mode 100644 custom-nginx/Dockerfile
 create mode 100644 custom-nginx/html/index.html
```

`git push origin main`에서 `main -> main`이 표시되어 업로드 성공을 확인하였다. 이후 스크린샷은 GitHub 웹사이트에서 직접 업로드하였다.

**증빙 자료:** GitHub Push 성공 · VS Code 연동

## 8. 보너스 과제 — Docker Compose로 NGINX 웹 서버 실행

### 실습 목적

Docker Compose 설정 파일(`compose.yaml`)을 사용하여 NGINX 컨테이너를 생성·실행하고, 실행 상태와 브라우저 접속 결과를 검증하였다. Dockerfile을 별도로 작성하지 않고 공식 `nginx:alpine` 이미지를 사용하였다.

### 실행 환경 및 설정

실습은 Windows PowerShell에서 수행하였다. `docker compose version` 명령으로 **Docker Compose v5.3.1**을 확인하였다. 실습 당시 USB 프로젝트 경로는 `D:\Codyssey\Codyssey AllinOne\E1-1-dev-workstation`이었다.

프로젝트 루트에 `compose.yaml` 파일을 생성하고 다음과 같이 작성하였다.

```yaml
services:
web:
image: nginx:alpine
ports:
-"8081:80"
```

`web` 서비스는 공식 NGINX 이미지를 사용하며, 호스트의 **8081 포트**를 컨테이너의 **80 포트**에 연결한다.

### 실행 명령 및 검증 결과

```powershell
docker compose up -d
docker compose ps
```

실행 결과 `nginx:alpine` 이미지가 다운로드되었고, Compose 네트워크와 `e1-1-dev-workstation-web-1` 컨테이너가 생성되었다. `docker compose ps`에서 컨테이너 상태가 **Up**으로 표시되었으며, `8081:80` 포트 매핑을 확인하였다.

Chrome 브라우저에서 `http://localhost:8081`에 접속한 결과 **Welcome to nginx!** 기본 페이지가 정상적으로 표시되었다. 이로써 Compose 설정 파일에 따른 컨테이너 실행과 HTTP 접속을 검증하였다.

### 증빙 자료

Docker Compose 실행 및 NGINX 접속 검증 이미지

**검증 범위:** `docker compose up -d`, `docker compose ps` 실행과 웹 브라우저 접속 성공을 확인하였다.

## 9. 트러블슈팅

### 사례 1. WSL Ubuntu에서 Docker 실행 문제

- **문제:** Ubuntu에서 Docker 명령을 정상 실행하기 어려웠음
- **원인 가설:** Docker Desktop의 WSL 통합 설정 또는 엔진 연결 문제
- **확인·해결:** Docker Desktop의 WSL 연동을 점검하고 Ubuntu에서 Docker 명령을 다시 실행
- **결과:** Docker 엔진 점검과 `hello-world` 실행 성공

### 사례 2. Docker 엔진 접근 권한 문제

- **문제:** Docker 엔진 접근 과정에서 권한 관련 오류 경험
- **원인 가설:** 실행 사용자·Docker 소켓 접근 권한 또는 통합 환경 설정
- **확인·해결:** 실행 환경과 권한을 점검한 후 Docker 명령 재실행
- **결과:** 컨테이너 실행·관리 명령 정상 동작

### 사례 3. GitHub CLI 브라우저 자동 실행 실패

- **문제:** `gh auth login`에서 브라우저 자동 실행 실패
- **오류 요약:** `xdg-open`, `wslview` 등 브라우저 실행 도구를 찾지 못함
- **원인:** WSL 환경에서 브라우저 실행 도구를 사용할 수 없었음
- **해결:** Windows 브라우저에서 GitHub 기기 인증 페이지를 직접 열어 승인
- **결과:** `Authentication complete`, `Logged in as PuffyCripsy` 확인

### 포트 충돌 발생 시 진단 방법 (참고)

```bash
docker ps --filter "publish=8080"
```

8080 포트가 이미 사용 중이라면 기존 컨테이너를 정리하거나 호스트 포트를 바꿔 실행할 수 있다. 이 항목은 **참고 절차**이며 실제 발생한 오류 사례와 구분되는 일반적인 진단 방법이다.

## 10. 실습 증빙 자료

GitHub 저장소의 `screenshots/` 폴더에 등록된 스크린샷 8개를 실습 증빙으로 연결하였다. 별도 이미지가 등록되지 않은 실습은 본문의 명령어와 실행 결과 기록을 기준으로 기술하였다.

| 실습 | 검증 대상 | 실제 등록된 스크린샷 |
| --- | --- | --- |
| 4 | 파일·디렉터리 권한 변경 | 실습4_권한변경.PNG |
| 6 | Docker 실행 확인 | 실습6_Docker 실행 확인.png |
| 7 | Ubuntu 컨테이너 실행 및 파일 생성 | 실습7_Ubuntu 컨테이너 실행 및 관리.png · 실습7_Ubuntu 컨테이너 파일 생성 및 확인.png |
| 10 | NGINX 8080 포트 매핑 | 실습10_웹서버_포트매핑_8080.png.png |
| 13 | GitHub Push 및 VS Code 연동 | 실습13_GitHub_Push성공.png · 실습13_VSCode_GitHub연동.png |
| 보너스 | Docker Compose NGINX 웹 서버 실행 | 보너스_Docker_Compose_웹서버_실행확인.png |

### 주요 실습 스크린샷

#### 실습 4 — 파일·디렉터리 권한 변경

실습4_권한변경.PNG

!실습4_권한변경.PNG

실습4_권한변경.PNG

#### 실습 6 — Docker 실행 확인

실습6_Docker 실행 확인.png

!실습6_Docker 실행 확인.png

실습6_Docker 실행 확인.png

#### 실습 7 — Ubuntu 컨테이너 실행 및 파일 생성

실습7_Ubuntu 컨테이너 실행 및 관리.png

!실습7_Ubuntu 컨테이너 실행 및 관리.png

실습7_Ubuntu 컨테이너 실행 및 관리.png

실습7_Ubuntu 컨테이너 파일 생성 및 확인.png

!실습7_Ubuntu 컨테이너 파일 생성 및 확인.png

실습7_Ubuntu 컨테이너 파일 생성 및 확인.png

#### 실습 10 — NGINX 8080 포트 매핑

실습10_웹서버_포트매핑_8080.png.png

!실습10_웹서버_포트매핑_8080.png.png

실습10_웹서버_포트매핑_8080.png.png

#### 실습 13 — GitHub Push 및 VS Code 연동

실습13_GitHub_Push성공.png

!실습13_GitHub_Push성공.png

실습13_GitHub_Push성공.png

실습13_VSCode_GitHub연동.png

!실습13_VSCode_GitHub연동.png

실습13_VSCode_GitHub연동.png

#### 보너스 — Docker Compose NGINX 웹 서버 실행

보너스_Docker_Compose_웹서버_실행확인.png

!보너스_Docker_Compose_웹서버_실행확인.png

보너스_Docker_Compose_웹서버_실행확인.png

## 11. 결론

Linux CLI를 이용한 파일·권한 관리, Docker 이미지와 컨테이너의 차이, Dockerfile을 통한 실행 환경 재현, 포트 매핑, 바인드 마운트, 볼륨 영속성, Git의 로컬 버전 관리와 GitHub의 원격 저장소 역할을 실습하였다. 실제 Dockerfile과 HTML 파일을 GitHub에 업로드했으며, README와 스크린샷을 통해 실습 절차와 검증 결과를 기록하였다.

**보너스 과제:** Docker Compose를 이용해 NGINX 컨테이너를 실행하고, 실행 상태 및 브라우저 접속을 검증하였다.

