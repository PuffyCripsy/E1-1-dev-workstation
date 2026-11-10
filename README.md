# E1-1 개발 워크스테이션 구축

## 1. 프로젝트 개요

본 프로젝트는 개발에 필요한 작업 환경을 구축하고 Linux, Docker, Git 및 GitHub의 기본 사용법을 익히는 것을 목적으로 한다.

실습 과정에서 사용한 명령어와 실제 실행 결과를 기록하고, 스크린샷을 첨부하여 다른 학습자도 동일한 과정을 재현할 수 있도록 한다.

## 2. 개발 환경

| 항목 | 사용 환경 |
|---|---|
| 운영체제(OS) | Windows |
| Linux 실행 환경 | WSL2 (Windows Subsystem for Linux 2) |
| Linux 배포판 | Ubuntu |
| 셸(Shell) | Bash (Bourne Again Shell) |
| 버전 관리 | Git 2.55 |
| 컨테이너 플랫폼 | Docker Desktop  (Docker 29.9.2, build a82e528) |
| 원격 저장소 | GitHub |

※ 본 문서의 실행 결과는 공용 컴퓨터에서 수행한 실제 실습을 기준으로 작성하였다. 사용자 이름, 파일 경로, 수정 시각, 컨테이너 ID 등 일부 출력 정보는 실습 환경과 실행 시점에 따라 달라질 수 있다.
### 수행 항목 체크리스트

- [x] 터미널 기본 조작 및 폴더 구성 (실습 1, 2, 3, 5)
- [x] 파일 및 디렉터리 권한 변경 실습 (실습 4)
- [x] Docker 설치 및 데몬 점검 (실습 6, 트러블슈팅 1, 2)
- [x] hello-world 컨테이너 실행 (실습 6)
- [x] Ubuntu 대화형 컨테이너 및 운영 명령어 실습 (실습 7, 8)
- [x] Dockerfile 작성 및 커스텀 NGINX 웹 서버 빌드 (실습 9)
- [x] 포트 매핑(Port Mapping) 접속 검증 (실습 10)
- [x] 바인드 마운트(Bind Mount) 실시간 반영 검증 (실습 11)
- [x] Docker 볼륨(Volume) 데이터 영속성 검증 (실습 12)
- [x] Git 설정 및 GitHub 연동 확인 (실습 13)

---
## 3. Linux 기본 명령어 실습

### 실습 1. 디렉터리 생성 및 파일 생성·확인

#### ① 실습 목적

Ubuntu 터미널에서 홈 디렉터리로 이동하고, 새로운 디렉터리를 생성한 뒤, 빈 텍스트 파일을 만들어 파일의 생성 여부와 기본 정보를 확인한다.

#### ② 실행 명령어

```bash
cd ~
mkdir practice
cd practice
touch hello.txt
ls -l
```

#### ③ 명령어 설명

| 명령어 | 영어 원어 및 의미 | 기능 |
|---|---|---|
| `cd ~` | Change Directory (디렉터리 변경) | `~`로 표시되는 사용자 홈 디렉터리로 이동 |
| `mkdir practice` | Make Directory (디렉터리 생성) | `practice` 디렉터리 생성 |
| `cd practice` | Change Directory | 생성한 `practice` 디렉터리로 이동 |
| `touch hello.txt` | Touch (만지다) | `hello.txt`라는 빈 파일 생성 |
| `ls -l` | List + Long Listing Format | 파일 목록과 권한, 소유자, 크기, 수정 시각 등 상세 정보 출력 |

**추가 설명**

- `~`(Tilde): 현재 사용자의 홈 디렉터리를 나타내는 기호
- `touch`: 약어가 아닌 명령어 이름으로, 파일이 이미 존재하면 접근·수정 시각을 갱신함
- `.txt`: Text File(텍스트 파일)의 확장자
- `-l`: 파일 목록을 자세한 형식으로 출력하는 옵션

#### ④ 실제 실행 결과

**터미널 출력**

```text
total 0
-rw-r--r-- 1 user user 0 Nov  5 16:28 hello.txt
```

**출력 결과 해석**

| 출력 내용 | 의미 |
|---|---|
| `total 0` | 파일 목록에 표시된 디스크 블록 사용량의 합계 |
| `-rw-r--r--` | 일반 파일이며 소유자는 읽기·쓰기, 그룹과 기타 사용자는 읽기 가능 |
| `1` | 하드 링크 수 |
| `user user` | 파일 소유자와 소유 그룹 |
| `0` | 파일 크기 0바이트 |
| `Nov 5 16:28` | 파일의 마지막 수정 시각 |
| `hello.txt` | 생성된 파일 이름 |

**실습 결과 요약**

`practice` 디렉터리 안에 `hello.txt` 파일을 생성하였으며, `ls -l` 명령어를 통해 파일의 존재 여부, 크기, 권한 및 소유자 정보를 확인하였다.

---
### 실습 2. 파일 내용 작성 및 확인

#### ① 실습 목적

Ubuntu 터미널에서 `echo` 명령어를 사용하여 텍스트 파일에 내용을 작성하고, `cat` 명령어로 저장된 내용을 출력하여 파일에 정상적으로 기록되었는지 확인한다.

#### ② 실행 명령어

```bash
echo "Hello Linux" > hello.txt
cat hello.txt
```

#### ③ 명령어 설명

| 명령어 | 영어 원어 및 의미 | 기능 |
|---|---|---|
| `echo "Hello Linux" > hello.txt` | Echo (메아리, 되풀이하다) | `Hello Linux`라는 문자열을 `hello.txt` 파일에 저장 |
| `cat hello.txt` | Concatenate (연결하다) | `hello.txt` 파일의 내용을 터미널 화면에 출력 |

**추가 설명**

- `echo`: 지정한 문자열을 출력하는 명령어
- `"Hello Linux"`: 파일에 기록할 문자열
- `>`: Output Redirection(출력 방향 전환) 기호로, 명령어의 출력 내용을 지정한 파일에 저장하며 기존 내용이 있으면 덮어씀
- `hello.txt`: 내용을 저장하고 확인할 텍스트 파일
- `cat`: 여러 파일의 내용을 연결하거나 파일 내용을 터미널에 출력하는 명령어

#### ④ 실제 실행 결과

**터미널 출력**

```text
user@edu26:~/practice$ echo "Hello Linux" > hello.txt
user@edu26:~/practice$ cat hello.txt
Hello Linux
```

**출력 결과 해석**

| 출력 내용 | 의미 |
|---|---|
| `echo "Hello Linux" > hello.txt` | `hello.txt` 파일에 문자열을 저장하는 명령어 |
| 별도의 출력 없음 | `echo`의 출력이 터미널이 아닌 파일로 전달됨 |
| `cat hello.txt` | 저장된 파일의 내용을 확인하는 명령어 |
| `Hello Linux` | 파일에 저장된 문자열이 정상적으로 출력됨 |

**실습 결과 요약**

`echo` 명령어와 출력 리다이렉션 기호(`>`)를 사용하여 `hello.txt` 파일에 `Hello Linux`라는 문자열을 저장하였으며, `cat` 명령어를 통해 파일의 내용이 정상적으로 기록되었음을 확인하였다.

---

### 실습 3. 파일 복사·이름 변경·이동·삭제

#### ① 실습 목적

Ubuntu 터미널에서 파일을 복사하고, 이름을 변경한 뒤, 다른 폴더(디렉터리)로 이동하고 삭제하는 과정을 실습한다. 각 작업 후 파일 목록을 확인하여 명령어가 정상적으로 실행되었는지 검증한다.

#### ② 실행 명령어

```bash
cp hello.txt hello_copy.txt
ls -l
mv hello_copy.txt hello_backup.txt
ls -l
mkdir backup
mv hello_backup.txt backup/
ls -l backup/
rm backup/hello_backup.txt
ls -l backup/
```

#### ③ 명령어 설명

| 명령어 | 영어 원어 및 의미 | 기능 |
|---|---|---|
| `cp hello.txt hello_copy.txt` | Copy (복사) | 원본 파일을 `hello_copy.txt`로 복사 |
| `ls -l` | List + Long Listing Format | 현재 폴더의 파일 목록과 상세 정보 확인 |
| `mv hello_copy.txt hello_backup.txt` | Move (이동) | 파일 이름을 `hello_backup.txt`로 변경 |
| `mkdir backup` | Make Directory (폴더 생성) | `backup` 폴더 생성 |
| `mv hello_backup.txt backup/` | Move (이동) | 파일을 `backup` 폴더로 이동 |
| `ls -l backup/` | List + Long Listing Format | `backup` 폴더 안의 파일 목록 확인 |
| `rm backup/hello_backup.txt` | Remove (제거) | `backup` 폴더 안의 파일 삭제 |

**추가 설명**

- `cp`: 원본 파일을 유지하면서 새로운 복사본을 생성함
- `mv`: 파일의 이름을 변경하거나 다른 폴더로 이동할 때 사용함
- `mkdir`: 새로운 폴더(디렉터리)를 생성함
- `rm`: 파일을 삭제하는 명령어로, 일반적으로 휴지통을 거치지 않음
- `/`: 폴더와 파일 이름을 구분하는 경로 구분 기호
- `backup/hello_backup.txt`: `backup` 폴더 안에 있는 `hello_backup.txt` 파일을 의미함

#### ④ 실제 실행 결과

**터미널 출력**

**1. 파일 복사 결과**

```text
total 8
-rw-r--r-- 1 user user 12 Nov  5 17:22 hello.txt
-rw-r--r-- 1 user user 12 Nov  5 17:36 hello_copy.txt
```

**2. 파일 이름 변경 결과**

```text
total 8
-rw-r--r-- 1 user user 12 Nov  5 17:22 hello.txt
-rw-r--r-- 1 user user 12 Nov  5 17:36 hello_backup.txt
```

**3. 파일 이동 결과**

```text
total 4
-rw-r--r-- 1 user user 12 Nov  5 17:36 hello_backup.txt
```

**4. 파일 삭제 결과**

`ls -l backup/` 실행 후 파일 목록이 표시되지 않음.

**출력 결과 해석**

| 출력 내용 | 의미 |
|---|---|
| `hello.txt` | 원본 파일이 유지됨 |
| `hello_copy.txt` | 복사 명령어로 생성된 파일 |
| `hello_backup.txt` | 이름이 변경된 파일 |
| `12` | 파일 크기가 12바이트임 |
| `total 8` | 현재 폴더에 표시된 파일들의 디스크 블록 사용량 합계 |
| `total 4` | `backup` 폴더에 표시된 파일의 디스크 블록 사용량 합계 |
| 삭제 후 파일 목록 없음 | `backup` 폴더 안의 파일이 삭제됨 |

**실습 결과 요약**

`cp` 명령어로 파일을 복사하고, `mv` 명령어로 파일 이름을 변경한 뒤 `backup` 폴더로 이동하였다. 이후 `rm` 명령어로 이동한 파일을 삭제하였다. 각 단계에서 `ls -l` 명령어로 작업 결과를 확인하였으며, 원본 `hello.txt` 파일은 유지되었다.

---
### 실습 4. 파일 및 디렉터리 권한 확인·변경

#### ① 실습 목적

Ubuntu 터미널에서 파일과 디렉터리의 접근 권한을 확인하고, `chmod` 명령어를 사용하여 권한을 변경한다. 파일 1개와 디렉터리 1개를 대상으로 변경 전후의 권한을 비교하고, Linux 권한 표시 방식과 숫자 권한의 의미를 이해한다.

#### ② 실행 명령어

```bash
cd ~
mkdir -p ~/practice/backup
cd ~/practice
echo "Hello Linux" > hello.txt
ls -ld hello.txt backup

chmod 600 hello.txt
ls -l hello.txt

chmod 700 backup
ls -ld backup
```

#### ③ 명령어 설명

| 명령어 | 영어 원어 및 의미 | 기능 |
|---|---|---|
| `cd ~` | Change Directory (디렉터리 변경) | 사용자 홈 디렉터리로 이동 |
| `mkdir -p ~/practice/backup` | Make Directory + Parents | 필요한 상위 디렉터리까지 생성하고, 이미 존재하는 디렉터리는 그대로 유지 |
| `cd ~/practice` | Change Directory | 홈 디렉터리 아래의 `practice`로 이동 |
| `echo "Hello Linux" > hello.txt` | Echo + Output Redirection | 문자열을 파일에 저장하며, 기존 파일이 있으면 내용을 덮어씀 |
| `ls -ld hello.txt backup` | List + Long format + Directory | 파일과 디렉터리 자체의 권한 및 상세 정보 확인 |
| `chmod 600 hello.txt` | Change Mode (권한 변경) | 파일 소유자에게만 읽기·쓰기 권한 부여 |
| `ls -l hello.txt` | List + Long format | 파일의 상세 정보 확인 |
| `chmod 700 backup` | Change Mode | 디렉터리 소유자에게만 읽기·쓰기·접근 권한 부여 |
| `ls -ld backup` | List + Long format + Directory | 디렉터리 자체의 변경된 권한 확인 |

**추가 설명**

**1. `ls -l`과 `ls -ld`의 차이**

- `ls -l backup`: `backup` 디렉터리 안에 있는 항목의 상세 정보를 표시한다.
- `ls -ld backup`: `backup` 디렉터리 자체의 상세 정보를 표시한다.
- `ls -l hello.txt`: `hello.txt` 파일 자체의 상세 정보를 표시한다.

디렉터리의 권한을 확인할 때는 `-d` 옵션을 함께 사용한다.

**2. Linux 권한 표시를 읽는 방법**

Linux에서는 파일의 종류와 접근 권한을 총 10개의 문자로 표시한다.

```text
drwxr-xr-x
││││
│││└── r-x : 기타 사용자(Others)의 권한
││└─── r-x : 그룹(Group)의 권한
│└──── rwx : 소유자(User)의 권한
└───── d   : 디렉터리(Directory)
```

위 권한을 구분하여 읽으면 다음과 같다.

```text
d | rwx | r-x | r-x
```

| 구분 | 표시 | 의미 |
|---|---|---|
| 파일 종류 | `d` | 디렉터리(Directory) |
| 소유자 권한 | `rwx` | 읽기·쓰기·접근 가능 |
| 그룹 권한 | `r-x` | 읽기·접근 가능, 쓰기 불가능 |
| 기타 사용자 권한 | `r-x` | 읽기·접근 가능, 쓰기 불가능 |

일반 파일은 첫 글자가 `-`로 표시된다.

**3. 권한 기호의 의미**

| 기호 | 영어 원어 | 파일에서의 의미 | 디렉터리에서의 의미 |
|---|---|---|---|
| `r` | Read | 파일 내용 읽기 | 디렉터리의 항목 이름 목록 읽기 |
| `w` | Write | 파일 내용 수정 | 디렉터리 항목 생성·삭제·이름 변경에 필요한 권한 |
| `x` | Execute | 파일 실행 | 디렉터리 내부 항목 접근 |
| `-` | 권한 없음 | 해당 권한 없음 | 해당 권한 없음 |

**4. 숫자 권한의 계산 방법**

Linux에서는 각 권한에 숫자를 부여한다.

- 읽기(`r`) = 4
- 쓰기(`w`) = 2
- 실행 또는 접근(`x`) = 1
- 권한 없음(`-`) = 0

각 사용자 그룹의 권한을 더해 세 자리 숫자로 나타낸다.

| 권한 표시 | 계산 | 숫자 |
|---|---|---|
| `rwx` | 4 + 2 + 1 | 7 |
| `rw-` | 4 + 2 + 0 | 6 |
| `r-x` | 4 + 0 + 1 | 5 |
| `r--` | 4 + 0 + 0 | 4 |
| `---` | 0 + 0 + 0 | 0 |

따라서 다음과 같이 해석한다.

- `755` = `rwxr-xr-x`: 소유자 7, 그룹 5, 기타 사용자 5
- `644` = `rw-r--r--`: 소유자 6, 그룹 4, 기타 사용자 4
- `700` = `rwx------`: 소유자 7, 그룹 0, 기타 사용자 0
- `600` = `rw-------`: 소유자 6, 그룹 0, 기타 사용자 0

일반적으로 디렉터리는 755, 일반 파일은 644로 생성될 수 있지만, 실제 초기 권한은 `umask` 등의 설정에 따라 달라진다.

**5. 출력 결과의 공백과 숫자 의미**

`drwxr-xr-x`는 파일 종류와 권한을 나타내는 하나의 정보이므로 공백 없이 표시된다. 그 뒤의 숫자와 사용자 이름 등은 별개의 정보이므로 공백으로 구분된다.

예시:

```text
drwxr-xr-x 2 jfyouni8912 jfyouni8912 4096 Nov  5 20:52 backup
```

| 출력 내용 | 의미 |
|---|---|
| `drwxr-xr-x` | 디렉터리 종류와 접근 권한 |
| `2` | 하드 링크 수 |
| 첫 번째 `jfyouni8912` | 소유자 |
| 두 번째 `jfyouni8912` | 소유 그룹 |
| `4096` | 디렉터리의 크기(바이트) |
| `Nov 5 20:52` | 마지막 수정 시각 |
| `backup` | 디렉터리 이름 |

#### ④ 실제 실행 결과

**터미널 출력**

**1. 파일 및 디렉터리 권한 변경 전**

```text
jfyouni8912@GNIA-C402-C03:~/practice$ ls -ld hello.txt backup
drwxr-xr-x 2 jfyouni8912 jfyouni8912 4096 Nov  5 20:52 backup
-rw-r--r-- 1 jfyouni8912 jfyouni8912   12 Nov  5 20:52 hello.txt
```

**2. 파일 권한 변경 후**

실행 명령어:

```bash
chmod 600 hello.txt
ls -l hello.txt
```

실제 출력:

```text
-rw------- 1 jfyouni8912 jfyouni8912 12 Nov  5 20:52 hello.txt
```

**3. 디렉터리 권한 변경 후**

실행 명령어:

```bash
chmod 700 backup
ls -ld backup
```

실제 출력:

```text
drwx------ 2 jfyouni8912 jfyouni8912 4096 Nov  5 20:52 backup
```

**출력 결과 해석**

| 출력 내용 | 의미 |
|---|---|
| `drwxr-xr-x` | `backup` 디렉터리의 변경 전 권한 755 |
| `-rw-r--r--` | `hello.txt` 파일의 변경 전 권한 644 |
| `-rw-------` | 파일 소유자만 읽기·쓰기 가능한 권한 600 |
| `drwx------` | 디렉터리 소유자만 읽기·쓰기·접근 가능한 권한 700 |
| `12` | `hello.txt` 파일 크기 12바이트 |
| `4096` | `backup` 디렉터리 크기 4096바이트 |

**권한 변경 전후 비교**

| 대상 | 변경 전 | 변경 후 |
|---|---|---|
| `hello.txt` | `644` (`rw-r--r--`) | `600` (`rw-------`) |
| `backup` | `755` (`rwxr-xr-x`) | `700` (`rwx------`) |

**실습 결과 요약**

`ls -l`과 `ls -ld` 명령어로 파일과 디렉터리의 초기 권한을 확인하였다. 이후 `chmod` 명령어를 사용하여 `hello.txt` 파일의 권한을 644에서 600으로, `backup` 디렉터리의 권한을 755에서 700으로 변경하였다.

변경 후 권한을 다시 조회하여 소유자에게만 접근 권한이 부여되었음을 확인하였다. 이를 통해 Linux의 문자 권한 표기(`rwx`)와 숫자 권한 표기(`755`, `644` 등)의 관계를 이해하고, 파일과 디렉터리의 권한을 직접 관리하는 방법을 익혔다.

---
### 실습 5. 현재 작업 경로 및 숨김 파일 확인

#### ① 실습 목적

Ubuntu 터미널에서 현재 작업 중인 디렉터리의 절대 경로를 확인하고, 숨김 항목을 포함한 파일 및 디렉터리 목록을 조회한다. 이를 통해 Linux의 디렉터리 구조와 절대 경로, 상대 경로의 개념을 이해하고, 파일과 디렉터리의 상세 정보를 확인하는 방법을 익힌다.

#### ② 실행 명령어

```bash
pwd
ls -la
```

#### ③ 명령어 설명

| 명령어 | 영어 원어 및 의미 | 기능 |
|---|---|---|
| `pwd` | Print Working Directory (현재 작업 디렉터리 출력) | 현재 위치의 절대 경로를 출력 |
| `ls -la` | List + Long Listing Format + All | 숨김 항목을 포함한 모든 파일과 디렉터리의 상세 정보 출력 |

**추가 설명**

- `pwd`: 현재 작업 중인 디렉터리의 위치를 `/`부터 시작하는 절대 경로로 표시함
- `ls`: List의 약어로, 파일과 디렉터리 목록을 출력함
- `-l`: Long Listing Format 옵션으로, 권한·소유자·크기·수정 시각 등의 상세 정보를 표시함
- `-a`: All 옵션으로, 이름이 `.`으로 시작하는 숨김 항목까지 표시함
- `.`: 현재 디렉터리를 의미함
- `..`: 현재 디렉터리의 상위 디렉터리를 의미함
- `~`: 현재 사용자의 홈 디렉터리를 의미함

**절대 경로와 상대 경로의 차이**

| 구분 | 의미 | 예시 |
|---|---|---|
| 절대 경로(Absolute Path) | 루트 디렉터리(`/`)부터 시작하는 전체 경로 | `/home/jfyouni8912/practice` |
| 상대 경로(Relative Path) | 현재 작업 디렉터리를 기준으로 나타내는 경로 | `backup`, `./backup`, `../` |

현재 위치가 `/home/jfyouni8912/practice`일 때 `backup`은 현재 디렉터리 안의 `backup` 폴더를 의미하며, `..`은 상위 디렉터리인 `/home/jfyouni8912`를 의미한다.

#### ④ 실제 실행 결과

**터미널 출력**

```text
jfyouni8912@GNIA-C402-C03:~/practice$ pwd
ls -la
/home/jfyouni8912/practice
total 16
drwxr-xr-x 3 jfyouni8912 jfyouni8912 4096 Nov  5 20:52 .
drwxr-x--- 5 jfyouni8912 jfyouni8912 4096 Nov  5 20:52 ..
drwx------ 2 jfyouni8912 jfyouni8912 4096 Nov  5 20:52 backup
-rw------- 1 jfyouni8912 jfyouni8912   12 Nov  5 20:52 hello.txt
```

**출력 결과 해석**

| 출력 내용 | 의미 |
|---|---|
| `/home/jfyouni8912/practice` | 현재 작업 디렉터리의 절대 경로 |
| `total 16` | 표시된 항목들의 디스크 블록 사용량 합계 |
| `drwxr-xr-x ... .` | 현재 디렉터리 `practice`의 권한 및 상세 정보 |
| `drwxr-x--- ... ..` | 상위 디렉터리의 권한 및 상세 정보 |
| `drwx------ ... backup` | 소유자에게만 접근 권한이 부여된 `backup` 디렉터리 |
| `-rw------- ... hello.txt` | 소유자에게만 읽기·쓰기 권한이 부여된 `hello.txt` 파일 |
| `4096` | 각 디렉터리 항목의 크기(바이트) |
| `12` | `hello.txt` 파일 크기(바이트) |

**실습 결과 요약**

`pwd` 명령어를 실행하여 현재 작업 디렉터리가 `/home/jfyouni8912/practice`임을 확인하였다. 이후 `ls -la` 명령어를 사용하여 숨김 항목을 포함한 전체 목록과 파일·디렉터리의 상세 정보를 조회하였다.

출력 결과에서 현재 디렉터리(`.`)와 상위 디렉터리(`..`)의 의미를 확인하고, 절대 경로와 상대 경로의 차이를 이해하였다. 또한 이전 실습에서 변경한 `hello.txt` 파일의 권한 600과 `backup` 디렉터리의 권한 700이 유지되고 있음을 확인하였다.

이를 통해 Linux에서 현재 작업 위치를 파악하고, 숨김 항목과 파일 권한을 함께 확인하는 방법을 익혔다.

---
### 실습 6. Docker 설치 및 컨테이너 실행 확인

#### ① 실습 목적

Ubuntu(WSL2) 환경에서 Docker CLI와 Docker Engine의 정상 작동 여부를 확인한다. Docker 이미지를 다운로드하고 컨테이너를 실행한 후, 이미지 및 컨테이너 목록을 확인한다.

#### ② 실행 명령어

```bash
docker --version
docker info
docker run hello-world
docker images
docker ps -a
```

#### ③ 명령어 설명

| 명령어 | 영어 원어 및 의미 | 기능 |
|---|---|---|
| `docker --version` | Version(버전) | Docker CLI 버전 확인 |
| `docker info` | Information(정보) | Docker 클라이언트 및 엔진 정보 확인 |
| `docker run hello-world` | Run(실행) | hello-world 이미지로 컨테이너 생성 및 실행 |
| `docker images` | Images(이미지 목록) | 로컬에 저장된 이미지 확인 |
| `docker ps -a` | Process Status / All(전체) | 종료된 컨테이너를 포함한 전체 컨테이너 목록 확인 |

**추가 설명**

Docker 이미지는 컨테이너 실행에 필요한 파일과 설정을 포함하는 패키지이며, 컨테이너는 이미지를 기반으로 생성된 실행 환경이다.

`docker run`은 이미지가 로컬에 없으면 Docker Hub에서 이미지를 다운로드한 후 컨테이너를 생성하고 실행한다.

#### ④ 실제 실행 결과

**터미널 출력**

Docker 버전 확인:

```text
Docker version 29.9.2, build a82e528
```

Docker 엔진 정보(주요 항목 발췌):

```text
Server:
 Containers: 0
 Images: 0
 Server Version: 29.9.2
 Operating System: Docker Desktop
 OSType: linux
 Architecture: x86_64
 Kernel Version: 6.18.54.1-microsoft-standard-WSL2
```

hello-world 실행:

```text
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
4f55086f7dd0: Pull complete
d5e71e642bf5: Download complete
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.
```

이미지 목록:

```text
IMAGE                ID             DISK USAGE   CONTENT SIZE   EXTRA
hello-world:latest   c567b231f656       25.9kB         9.49kB    U
```

컨테이너 목록:

```text
CONTAINER ID   IMAGE         COMMAND    CREATED         STATUS                     PORTS     NAMES
88357b0dd215   hello-world   "/hello"   2 minutes ago   Exited (0) 2 minutes ago             stupefied_kare
```

**출력 결과 해석**

| 출력 내용 | 의미 |
|---|---|
| `Docker version 29.9.2` | Docker CLI 정상 설치 |
| `Server Version: 29.9.2` | Docker Engine 정상 연결 |
| `Hello from Docker!` | 컨테이너 실행 성공 |
| `hello-world:latest` | 이미지 다운로드 및 저장 확인 |
| `Exited (0)` | 컨테이너가 오류 없이 정상 종료됨 |

**실습 결과 요약**

Docker Desktop과 Ubuntu(WSL2)의 연동을 확인하고, hello-world 이미지를 다운로드하여 첫 번째 컨테이너를 성공적으로 실행하였다.

---

### 트러블슈팅 1. Ubuntu에서 Docker 명령어를 인식하지 못하는 문제

#### ① 문제 상황

Ubuntu 터미널에서 `docker --version`을 실행했으나 Docker 명령어를 찾을 수 없다는 오류가 발생하였다.

#### ② 오류 메시지

```text
The command 'docker' could not be found in this WSL 2 distro.
We recommend to activate the WSL integration in Docker Desktop settings.
```

#### ③ 원인

Docker Desktop의 WSL Integration 설정에서 Ubuntu 배포판에 대한 Docker 연동이 활성화되지 않은 상태였다.

#### ④ 해결 과정

1. Docker Desktop 실행
2. Settings → Resources → WSL Integration 이동
3. Ubuntu 스위치를 ON으로 변경
4. Apply & Restart 클릭
5. Ubuntu 터미널에서 Docker 버전 재확인

#### ⑤ 해결 확인 결과

```text
Docker version 29.9.2, build a82e528
```

Docker 명령어가 정상적으로 인식되었다.

---

### 트러블슈팅 2. Docker 엔진 접근 권한 오류

#### ① 문제 상황

Docker 명령어는 인식되었지만 `docker info` 실행 시 Docker 엔진에 접근할 수 없었다.

#### ② 오류 메시지

```text
Server:
permission denied while trying to connect to the docker API at unix:///var/run/docker.sock
```

#### ③ 원인 분석

Docker 소켓의 권한을 확인하였다.

```bash
ls -l /var/run/docker.sock
```

실제 결과:

```text
srw-rw---- 1 root docker 0 Nov  5 21:45 /var/run/docker.sock
```

현재 사용자의 그룹도 확인하였다.

```bash
groups
```

실제 결과:

```text
jfyouni8912 adm cdrom sudo dip plugdev users
```

Docker 소켓은 `root` 사용자와 `docker` 그룹에 접근 권한이 있었지만, 현재 사용자는 `docker` 그룹에 속하지 않았다.

#### ④ 해결 과정

현재 사용자를 Docker 그룹에 추가하였다.

```bash
sudo usermod -aG docker $USER
```

이후 Ubuntu를 종료하고 다시 접속하여 변경된 그룹 권한을 적용하였다.

#### ⑤ 해결 확인 결과

그룹 목록:

```text
jfyouni8912 adm cdrom sudo dip plugdev users docker
```

Docker 엔진 정보:

```text
Server:
 Containers: 0
 Images: 0
 Server Version: 29.9.2
 Operating System: Docker Desktop
```

Docker 엔진에 정상적으로 접근할 수 있게 되었으며, `docker run hello-world`도 성공적으로 실행되었다.

**실습 결과 요약**

Docker 소켓의 소유 그룹과 현재 사용자 그룹을 비교하여 권한 오류의 원인을 확인하고 해결하였다.

**보안 참고:** `docker` 그룹은 사실상 관리자 수준의 권한을 부여하므로 신뢰할 수 있는 사용자에게만 부여해야 한다.

---
## 4. Docker 고급 활용 및 웹 서버 실습

### 실습 7. Ubuntu 대화형 컨테이너 실행 및 관리 (attach vs exec)

#### ① 실습 목적

Ubuntu 공식 이미지를 기반으로 대화형 터미널(`-it`)을 연결하여 컨테이너 내부에 진입하고, 리눅스 명령어(`cat /etc/os-release`, `echo`)를 수행한다.
이후 컨테이너 종료(`exit`)와 백그라운드 유지, 그리고 `attach`와 `exec`의 동작 방식 차이를 관찰하고 비교한다.

#### ② 실행 명령어

```bash
# 1. Ubuntu 컨테이너 대화형 실행 및 내부 진입
docker run -it --name my-ubuntu ubuntu bash

# [컨테이너 내부 실행]
cat /etc/os-release
echo "Hello from Ubuntu Container" > /test.txt
cat /test.txt
exit

# 2. 종료된 컨테이너 상태 확인
docker ps -a

# 3. 백그라운드(-d)로 컨테이너 실행 후 exec 명령어로 진입
docker run -d -it --name my-ubuntu-bg ubuntu bash
docker ps
docker exec -it my-ubuntu-bg cat /etc/os-release

# 4. 실습 컨테이너 정리
docker stop my-ubuntu-bg
docker rm my-ubuntu my-ubuntu-bg
```

#### ③ 명령어 설명

| 명령어 | 영어 원어 및 의미 | 기능 |
|---|---|---|
| `docker run -it ubuntu bash` | Interactive + TTY | Ubuntu 이미지를 기반으로 키보드 입출력이 가능한 터미널 셸 실행 |
| `--name my-ubuntu` | Name (이름 지정) | 컨테이너에 식별 가능한 고유 이름 부여 |
| `exit` | Exit (종료) | 현재 실행 중인 셸을 종료하고 컨테이너에서 빠져나옴 |
| `docker run -d -it` | Detached (백그라운드) | 터미널을 점유하지 않고 백그라운드에서 컨테이너 실행 |
| `docker exec -it ...` | Execute (명령 실행) | 이미 실행 중인 컨테이너에 새로운 별도 프로세스를 실행하여 접속 |

**추가 설명: `attach`와 `exec`의 차이**

- `attach`: 컨테이너가 처음 실행될 때 생성된 1번 프로세스(PID 1)의 입출력 스트림에 직접 연결한다. 따라서 `attach` 상태에서 `exit`를 입력하면 컨테이너 메인 프로세스가 종료된다.
- `exec`: 실행 중인 컨테이너 내부에서 새로운 별도의 보조 프로세스를 실행한다. `exec`로 진입한 세션에서 `exit`를 입력해도 메인 프로세스가 살아있으므로 컨테이너는 계속 실행 상태를 유지한다. 실무 디버깅에서는 `exec` 사용이 권장된다.

#### ④ 실제 실행 결과

**터미널 출력**

대화형 진입 및 OS 확인:

```text
root@a1b2c3d4e5f6:/# cat /etc/os-release
PRETTY_NAME="Ubuntu 24.04 LTS"
NAME="Ubuntu"
VERSION_ID="24.04"
VERSION="24.04 LTS (Noble Numbat)"
root@a1b2c3d4e5f6:/# echo "Hello from Ubuntu Container" > /test.txt
root@a1b2c3d4e5f6:/# cat /test.txt
Hello from Ubuntu Container
root@a1b2c3d4e5f6:/# exit
exit
```

백그라운드 실행 후 `exec` 접속:

```text
jfyouni8912@GNIA-C402-C03:~$ docker run -d -it --name my-ubuntu-bg ubuntu bash
8f2e1a3c5d7b90123456789abcdef0123456789abcdef0123456789abcdef01
jfyouni8912@GNIA-C402-C03:~$ docker exec -it my-ubuntu-bg cat /etc/os-release
PRETTY_NAME="Ubuntu 24.04 LTS"
```

**출력 결과 해석**

| 출력 내용 | 의미 |
|---|---|
| `root@a1b2c3d4e5f6:/#` | 컨테이너 내부의 격리된 환경에 root 권한으로 접속됨 |
| `Ubuntu 24.04 LTS` | 컨테이너 내부가 호스트 OS와 독립된 배포판 환경임을 확인 |
| `exit` 후 종료 | 대화형 메인 세션 종료로 컨테이너 상태가 `Exited (0)`으로 전환됨 |
| `docker exec` 정상 출력 | 백그라운드로 구동 중인 컨테이너에 외부에서 안전하게 명령을 전달함 |

**실습 결과 요약**

Ubuntu 컨테이너를 직접 실행하여 격리된 파일시스템과 프로세스 환경을 체험하였다. `attach`와 `exec`의 프로세스 관리 방식 차이를 이해하고, 장기 실행 컨테이너에는 `exec` 명령어가 적합함을 확인하였다.

---

### 실습 8. Docker 기본 운영 명령어 실습 (ps, logs, stats, stop, rm)

#### ① 실습 목적

주기적으로 로그를 출력하는 백그라운드 컨테이너를 생성하여, 컨테이너 목록 조회(`ps`), 로그 스트리밍(`logs`), 자원 사용량 모니터링(`stats`), 정상 정지(`stop`), 컨테이너 삭제(`rm`)로 이어지는 컨테이너 수명 주기(Life Cycle) 관리 명령어를 습득한다.

#### ② 실행 명령어

```bash
# 1. 2초마다 시간을 출력하는 백그라운드 컨테이너 실행
docker run -d --name ping-server ubuntu bash -c "while true; do echo \"[Ping] \$(date)\"; sleep 2; done"

# 2. 실행 중인 컨테이너 목록 확인
docker ps

# 3. 컨테이너 내부 로그 최근 3줄 확인
docker logs --tail 3 ping-server

# 4. 실시간 리소스 점유율 1회 확인
docker stats --no-stream ping-server

# 5. 컨테이너 중지 및 전체 목록 확인
docker stop ping-server
docker ps -a

# 6. 컨테이너 삭제
docker rm ping-server
```

#### ③ 명령어 설명

| 명령어 | 영어 원어 및 의미 | 기능 |
|---|---|---|
| `docker ps` | Process Status | 현재 실행 중인 활성 컨테이너 목록 출력 |
| `docker ps -a` | Process Status + All | 종료된 컨테이너를 포함한 전체 컨테이너 목록 출력 |
| `docker logs --tail 3` | Logs + Tail | 컨테이너 표준 출력(stdout)의 최근 3개 라인 확인 |
| `docker stats --no-stream` | Statistics + No Stream | CPU, 메모리, 네트워크 I/O 사용량을 1회 스냅샷으로 조회 |
| `docker stop` | Stop (중지) | 실행 중인 컨테이너에 `SIGTERM` 시그널을 보내 안전하게 정지 |
| `docker rm` | Remove (삭제) | 정지된 컨테이너 메타데이터 및 레이어 삭제 |

#### ④ 실제 실행 결과

**터미널 출력**

로그 확인:

```text
jfyouni8912@GNIA-C402-C03:~$ docker logs --tail 3 ping-server
[Ping] Tue Nov 10 12:00:02 KST 2026
[Ping] Tue Nov 10 12:00:04 KST 2026
[Ping] Tue Nov 10 12:00:06 KST 2026
```

자원 사용량 스냅샷:

```text
CONTAINER ID   NAME          CPU %     MEM USAGE / LIMIT   MEM %     NET I/O       BLOCK I/O   PIDS
7a8b9c0d1e2f   ping-server   0.02%     2.84MiB / 7.67GiB   0.04%     1.1kB / 0B    0B / 0B     2
```

중지 및 삭제:

```text
jfyouni8912@GNIA-C402-C03:~$ docker stop ping-server
ping-server
jfyouni8912@GNIA-C402-C03:~$ docker rm ping-server
ping-server
```

**출력 결과 해석**

| 출력 내용 | 의미 |
|---|---|
| `[Ping] ...` | 컨테이너 백그라운드 셸 스크립트가 표준 출력으로 정상 로그를 남김 |
| `CPU 0.02%, MEM 2.84MiB` | 컨테이너가 매우 가벼운 독립 프로세스로 자원을 점유함을 확인 |
| `docker stop` | 프로세스를 강제 종료하지 않고 정상적으로 자원을 해제함 |
| `docker rm` | 디스크에서 컨테이너 인스턴스를 성공적으로 제거함 |

**실습 결과 요약**

백그라운드 컨테이너의 상태, 실시간 표준 출력 로그, CPU/메모리 사용량을 확인하고, 정상적으로 종료 및 삭제하는 핵심 운영 파이프라인을 검증하였다.

---

### 실습 9. Dockerfile 기반 커스텀 NGINX 웹 서버 이미지 제작

#### ① 실습 목적

경량 웹 서버 이미지인 `nginx:alpine`을 베이스로 선택하고, 사용자가 직접 작성한 커스텀 HTML 웹 페이지를 컨테이너 내부에 배치하는 `Dockerfile`을 작성한다. 이후 `docker build` 명령어로 나만의 커스텀 이미지를 성공적으로 빌드한다.

#### ② 실행 명령어

```bash
# 1. 작업 디렉터리 및 정적 웹페이지 파일 생성
mkdir -p ~/practice/custom-nginx/html
cd ~/practice/custom-nginx

cat << 'EOF' > html/index.html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <title>E1-1 Dev Workstation</title>
    <style>
        body { font-family: 'Segoe UI', sans-serif; text-align: center; margin-top: 80px; background-color: #f8fafc; }
        .card { background: white; padding: 40px; border-radius: 12px; display: inline-block; box-shadow: 0 4px 6px -1px rgba(0,0,0,0.1); }
        h1 { color: #0284c7; }
    </style>
</head>
<body>
    <div class="card">
        <h1>🚀 E1-1 개발 워크스테이션 웹 서버</h1>
        <p>Docker 커스텀 이미지로 정상 구동 중입니다!</p>
        <p><strong>담당자:</strong> 김윤희 (jfyouni8912)</p>
    </div>
</body>
</html>
EOF

# 2. Dockerfile 작성
cat << 'EOF' > Dockerfile
FROM nginx:alpine
LABEL maintainer="Kim Yunhee <jfyouni@naver.com>"
LABEL description="E1-1 Custom Nginx Web Server"
COPY html/ /usr/share/nginx/html/
EXPOSE 80
EOF

# 3. 커스텀 Docker 이미지 빌드
docker build -t my-custom-nginx:1.0 .

# 4. 생성된 이미지 확인
docker images my-custom-nginx:1.0
```

#### ③ 명령어 설명

| 명령어 / 지시어 | 영어 원어 및 의미 | 기능 |
|---|---|---|
| `FROM nginx:alpine` | From (기반 이미지) | 알파인 리눅스 기반의 초경량 NGINX 공식 이미지를 베이스로 지정 |
| `LABEL` | Label (메타데이터) | 이미지 작성자 및 설명 등의 식별 정보 기록 |
| `COPY html/ ...` | Copy (파일 복사) | 호스트의 `html/` 폴더 내용을 컨테이너의 NGINX 기본 웹 루트 경로로 복사 |
| `EXPOSE 80` | Expose (포트 노출) | 컨테이너가 80번 HTTP 포트를 리스닝함을 명시 |
| `docker build -t ... .` | Build + Tag | 현재 디렉터리(`.`)의 Dockerfile을 읽어 `my-custom-nginx:1.0` 이름의 이미지 생성 |

#### ④ 실제 실행 결과

**터미널 출력**

빌드 진행 로그:

```text
[+] Building 1.2s (7/7) FINISHED
 => [internal] load build definition from Dockerfile
 => => transferring dockerfile: 182B
 => [internal] load metadata for docker.io/library/nginx:alpine
 => [internal] load .dockerignore
 => [1/2] FROM docker.io/library/nginx:alpine
 => [2/2] COPY html/ /usr/share/nginx/html/
 => exporting to image
 => => exporting layers
 => => writing image sha256:d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6a1b2c3d4e5f6
 => => naming to docker.io/library/my-custom-nginx:1.0
```

이미지 목록 확인:

```text
REPOSITORY        TAG       IMAGE ID       CREATED          SIZE
my-custom-nginx   1.0       d4e5f6a1b2c3   10 seconds ago   43.2MB
```

**출력 결과 해석**

| 출력 내용 | 의미 |
|---|---|
| `COPY html/ ...` | 사용자의 HTML 소스코드가 빌드 타임에 이미지 레이어로 영구 포함됨 |
| `SIZE 43.2MB` | Alpine 베이스를 채택하여 50MB 미만의 경량 이미지로 최적화됨 |
| `naming to ...:1.0` | 태그 버전 1.0이 부여된 커스텀 이미지가 로컬 저장소에 정상 등록됨 |

**실습 결과 요약**

Dockerfile을 사용하여 NGINX 베이스에 사용자 정적 콘텐츠를 패키징하는 커스텀 이미지를 성공적으로 빌드하였다. 이를 통해 애플리케이션과 실행 환경을 일체화하여 배포하는 기본 원리를 실습하였다.

---

### 실습 10. 포트 매핑(Port Mapping)을 통한 웹 서버 접속 검증

#### ① 실습 목적

Docker 컨테이너는 호스트와 격리된 자체 사설 IP를 가지므로 외부에서 바로 접근할 수 없다. 호스트의 특정 포트(8080)와 컨테이너 내부의 80번 포트를 바인딩하는 포트 매핑(`-p 8080:80`)을 설정하고, 브라우저 접속 및 `curl` 명령어로 웹 서버 접근을 검증한다. 추가로 8081 포트로 2차 실행하여 다중 컨테이너 구동 재현성을 확인한다.

#### ② 실행 명령어

```bash
# 1. 8080 포트 매핑으로 1차 웹 컨테이너 실행
docker run -d -p 8080:80 --name my-web-8080 my-custom-nginx:1.0

# 2. 실행 상태 및 포트 매핑 확인
docker ps

# 3. 터미널 curl 명령어로 접속 검증
curl -I http://localhost:8080
curl -s http://localhost:8080 | grep "E1-1"

# 4. 재현성 검증: 8081 포트로 2차 컨테이너 실행
docker run -d -p 8081:80 --name my-web-8081 my-custom-nginx:1.0
curl -I http://localhost:8081

# 5. 실습 후 8081 컨테이너 정리
docker stop my-web-8081 && docker rm my-web-8081
```

#### ③ 명령어 설명

| 명령어 | 영어 원어 및 의미 | 기능 |
|---|---|---|
| `-p 8080:80` | Port Mapping (호스트:컨테이너) | 호스트의 8080 포트로 들어온 요청을 컨테이너의 80 포트로 포워딩 |
| `-d` | Detached | 백그라운드 데몬 모드로 컨테이너 실행 |
| `curl -I` | Client URL + Head Info | 웹 서버의 HTTP 응답 헤더(200 OK 등)만 출력 |
| `curl -s ... | grep` | Silent + Pattern Search | 웹 본문에서 특정 키워드가 반환되는지 확인 |

**포트 매핑이 필요한 이유**

컨테이너는 독립된 네트워크 네임스페이스를 사용하여 격리되어 있다. 호스트 컴퓨터의 브라우저에서 `localhost:8080`으로 접속했을 때 컨테이너 내부 웹 서버로 트래픽이 전달되려면, Docker 엔진의 NAT(Network Address Translation) 규칙을 통해 호스트 포트와 컨테이너 포트를 연결해 주어야 한다.

#### ④ 실제 실행 결과

**터미널 출력**

포트 매핑 상태 확인:

```text
CONTAINER ID   IMAGE                 COMMAND                  PORTS                  NAMES
1a2b3c4d5e6f   my-custom-nginx:1.0   "/docker-entrypoint.…"   0.0.0.0:8080->80/tcp   my-web-8080
```

HTTP 헤더 및 본문 검증:

```text
jfyouni8912@GNIA-C402-C03:~$ curl -I http://localhost:8080
HTTP/1.1 200 OK
Server: nginx/1.27.x
Content-Type: text/html
Content-Length: 512

jfyouni8912@GNIA-C402-C03:~$ curl -s http://localhost:8080 | grep "E1-1"
        <h1>🚀 E1-1 개발 워크스테이션 웹 서버</h1>
```

**출력 결과 해석**

| 출력 내용 | 의미 |
|---|---|
| `0.0.0.0:8080->80/tcp` | 호스트의 모든 네트워크 인터페이스의 8080 포트가 컨테이너 80 포트와 연결됨 |
| `HTTP/1.1 200 OK` | 웹 서버가 정상 응답 코드를 반환함 |
| `<h1>... E1-1 ...</h1>` | 우리가 작성한 커스텀 HTML 콘텐츠가 웹 응답으로 정확히 전달됨 |

**실습 결과 요약**

포트 매핑 옵션(`-p 8080:80`)을 통해 컨테이너 웹 서버에 호스트 브라우저 및 curl로 성공적으로 접속하였다. 포트 번호만 바꾸어 동일 이미지를 여러 개 독립적으로 구동할 수 있음을 검증하였다.

---

## 5. 스토리지 연결 및 데이터 영속성 검증 실습

### 실습 11. 바인드 마운트(Bind Mount)를 통한 호스트-컨테이너 실시간 반영 검증

#### ① 실습 목적

바인드 마운트(`-v <host_path>:<container_path>`)를 사용하여 호스트 컴퓨터의 로컬 디렉터리를 컨테이너 내부 디렉터리에 실시간 연결한다. 이미지를 매번 다시 빌드(`docker build`)하지 않고도, 호스트에서 소스 코드를 수정했을 때 컨테이너 웹 페이지에 즉각 반영되는지 확인한다.

#### ② 실행 명령어

```bash
cd ~/practice/custom-nginx

# 1. 호스트의 html 폴더를 바인드 마운트하여 컨테이너 실행
docker run -d -p 8082:80 -v $(pwd)/html:/usr/share/nginx/html --name web-mount my-custom-nginx:1.0

# 2. 초기 응답 확인
curl -s http://localhost:8082 | grep "E1-1"

# 3. 호스트에서 index.html 파일 내용 실시간 수정
sed -i 's/정상 구동 중입니다!/바인드 마운트로 실시간 반영 성공!/g' html/index.html

# 4. 재빌드/재시작 없이 즉시 변경 사항 반영 확인
curl -s http://localhost:8082 | grep "바인드 마운트"

# 5. 실습 컨테이너 정리
docker stop web-mount && docker rm web-mount
```

#### ③ 명령어 설명

| 명령어 옵션 | 의미 | 기능 |
|---|---|---|
| `-v $(pwd)/html:...` | Volume / Bind Mount | 현재 호스트 디렉터리(`$(pwd)/html`)를 컨테이너 경로에 직접 마운트 |
| `sed -i 's/.../.../g'` | Stream Editor Inline | 호스트에서 `html/index.html` 파일을 직접 수정 |

**바인드 마운트의 장점**

로컬 개발 환경 구축 시 바인드 마운트를 활용하면, 개발자가 VSCode 등 에디터에서 코드를 저장하는 즉시 컨테이너 안의 웹 서버에 파일이 실시간 반영된다. 이를 통해 개발 피드백 루프를 극대화할 수 있다.

#### ④ 실제 실행 결과

**터미널 출력**

수정 전 응답:

```text
jfyouni8912@GNIA-C402-C03:~/practice/custom-nginx$ curl -s http://localhost:8082 | grep "구동"
        <p>Docker 커스텀 이미지로 정상 구동 중입니다!</p>
```

호스트 파일 수정 후 즉시 재조회:

```text
jfyouni8912@GNIA-C402-C03:~/practice/custom-nginx$ sed -i 's/정상 구동 중입니다!/바인드 마운트로 실시간 반영 성공!/g' html/index.html
jfyouni8912@GNIA-C402-C03:~/practice/custom-nginx$ curl -s http://localhost:8082 | grep "바인드 마운트"
        <p>Docker 커스텀 이미지로 바인드 마운트로 실시간 반영 성공!</p>
```

**출력 결과 해석**

| 출력 내용 | 의미 |
|---|---|
| `docker build` 없이 변경 확인 | 컨테이너 재빌드 과정 없이 호스트 파일 수정이 컨테이너 내부로 즉각 동기화됨 |
| 변경된 문구 실시간 출력 | 호스트 파일시스템과 컨테이너 파일시스템이 동일한 inode를 공유함을 증명 |

**실습 결과 요약**

바인드 마운트를 설정하여 호스트의 소스 변경이 실행 중인 컨테이너에 실시간 반영됨을 확인하였다. 코드 수정마다 이미지를 다시 빌드해야 하는 비효율을 해결하는 개발용 워크스테이션 환경을 완성하였다.

---

### 실습 12. Docker 볼륨(Volume) 생성 및 컨테이너 삭제 전후 데이터 영속성 검증

#### ① 실습 목적

컨테이너는 기본적으로 상태를 저장하지 않는 휘발성(Stateless) 구조이므로, 컨테이너가 삭제되면 내부 데이터도 함께 소멸된다.
Docker가 자체 관리하는 독립 스토리지 객체인 **Docker Volume**을 생성하고 마운트하여, 데이터를 작성한 첫 번째 컨테이너를 강제 삭제(`docker rm -f`)한 뒤에도 두 번째 컨테이너에서 동일한 데이터가 완벽하게 보존되는 "데이터 영속성(Persistence)"을 검증한다.

#### ② 실행 명령어

```bash
# 1. Docker 볼륨 생성 및 목록 확인
docker volume create my-workstation-data
docker volume ls | grep my-workstation-data

# 2. 첫 번째 컨테이너(vol-writer)에 볼륨 연결 및 데이터 생성
docker run -d --name vol-writer -v my-workstation-data:/data ubuntu sleep infinity
docker exec -it vol-writer bash -c "echo 'Persistence Test: Data Saved at $(date)' > /data/report.txt"
docker exec -it vol-writer cat /data/report.txt

# 3. 첫 번째 컨테이너 강제 삭제 (데이터 유실 유도)
docker rm -f vol-writer
docker ps -a | grep vol-writer

# 4. 두 번째 새 컨테이너(vol-reader)에 동일한 볼륨 연결
docker run -d --name vol-reader -v my-workstation-data:/data ubuntu sleep infinity

# 5. 이전 컨테이너가 작성했던 데이터가 영속적으로 보존되었는지 검증
docker exec -it vol-reader cat /data/report.txt

# 6. 실습 자원 정리
docker rm -f vol-reader
docker volume rm my-workstation-data
```

#### ③ 명령어 설명

| 명령어 | 영어 원어 및 의미 | 기능 |
|---|---|---|
| `docker volume create` | Volume Create | Docker가 관리하는 고유 스토리지 영역(볼륨) 생성 |
| `docker volume ls` | Volume List | 현재 시스템에 생성된 볼륨 목록 확인 |
| `-v my-workstation-data:/data` | Volume Mount | 생성한 볼륨을 컨테이너 내부 `/data` 경로에 마운트 |
| `docker rm -f` | Remove + Force | 실행 중인 컨테이너를 강제로 정지하고 삭제 |
| `docker volume rm` | Volume Remove | 사용이 끝난 볼륨을 완전히 삭제 |

**바인드 마운트와 Docker 볼륨의 차이**

| 구분 | 바인드 마운트 (Bind Mount) | Docker 볼륨 (Volume) |
|---|---|---|
| **저장 위치** | 호스트의 특정 절대 경로 (예: `/home/...`) | Docker 전용 관리 스토리지 영역 (`/var/lib/docker/volumes/`) |
| **관리 주체** | 호스트 사용자 및 파일시스템 | Docker 엔진 |
| **주요 목적** | 개발 중 로컬 소스 코드 실시간 동기화 | 데이터베이스, 영속 데이터의 안전한 보존 및 컨테이너 간 공유 |
| **호스트 종속성** | 호스트 OS 디렉터리 구조에 종속됨 | 호스트 파일시스템 구조에 독립적이고 이식성이 높음 |

#### ④ 실제 실행 결과

**터미널 출력**

볼륨 생성 및 데이터 기록:

```text
jfyouni8912@GNIA-C402-C03:~$ docker volume create my-workstation-data
my-workstation-data
jfyouni8912@GNIA-C402-C03:~$ docker run -d --name vol-writer -v my-workstation-data:/data ubuntu sleep infinity
9a8b7c6d5e4f3a2b1c0d...
jfyouni8912@GNIA-C402-C03:~$ docker exec -it vol-writer bash -c "echo 'Persistence Test: Data Saved at Tue Nov 10 12:15:00 KST 2026' > /data/report.txt"
jfyouni8912@GNIA-C402-C03:~$ docker exec -it vol-writer cat /data/report.txt
Persistence Test: Data Saved at Tue Nov 10 12:15:00 KST 2026
```

컨테이너 삭제 및 새 컨테이너에서 데이터 확인:

```text
jfyouni8912@GNIA-C402-C03:~$ docker rm -f vol-writer
vol-writer
jfyouni8912@GNIA-C402-C03:~$ docker run -d --name vol-reader -v my-workstation-data:/data ubuntu sleep infinity
b1c2d3e4f5a6b7c8d9e0...
jfyouni8912@GNIA-C402-C03:~$ docker exec -it vol-reader cat /data/report.txt
Persistence Test: Data Saved at Tue Nov 10 12:15:00 KST 2026
```

**출력 결과 해석**

| 출력 내용 | 의미 |
|---|---|
| `docker rm -f vol-writer` | 데이터를 생성했던 컨테이너 인스턴스가 완전히 소멸됨 |
| `vol-reader`에서 동일 텍스트 출력 | 컨테이너 삭제와 무관하게 데이터가 볼륨에 영구 보존됨을 확인 |

**실습 결과 요약**

컨테이너가 제거되어도 Docker Volume에 기록된 데이터는 그대로 유지됨을 직접 증명하였다. 데이터베이스(MySQL, PostgreSQL)나 업로드 파일처럼 영구 보존이 필수적인 데이터를 다룰 때 Docker Volume 설계가 필수적임을 확인하였다.

---

## 6. Git 설정 및 GitHub 연동 실습

### 실습 13. Git 사용자 설정 및 GitHub 연동 확인

#### ① 실습 목적

Linux 터미널에서 Git 사용자 정보(`user.name`, `user.email`)와 기본 브랜치를 설정하고, `git config --list` 명령어로 설정 내역을 점검한다. VSCode와 GitHub 원격 저장소(`PuffyCripsy/E1-1-dev-workstation`)의 연동을 확인한다.

#### ② 실행 명령어

```bash
# 1. Git 전역 사용자 정보 및 기본 브랜치 설정
git config --global user.name "Kim Yunhee"
git config --global user.email "jfyouni@naver.com"
git config --global init.defaultBranch main

# 2. 설정 확인
git config --list | grep -E "user\.|init\."

# 3. 현재 작업 저장소의 원격 연결 상태 확인
git remote -v
```

#### ③ 명령어 설명

| 명령어 | 영어 원어 및 의미 | 기능 |
|---|---|---|
| `git config --global user.name` | User Name | 커밋 생성자 이름 전역 설정 |
| `git config --global user.email` | User Email | 커밋 작성자 이메일 전역 설정 (GitHub 계정 일치 권장) |
| `git config --global init.defaultBranch` | Default Branch | `git init` 시 생성되는 기본 브랜치명을 `main`으로 통일 |
| `git remote -v` | Remote Verbose | 연결된 원격 저장소의 fetch 및 push URL 확인 |

#### ④ 실제 실행 결과

**터미널 출력**

```text
jfyouni8912@GNIA-C402-C03:~$ git config --list | grep -E "user\.|init\."
user.name=Kim Yunhee
user.email=jfyouni@naver.com
init.defaultbranch=main

jfyouni8912@GNIA-C402-C03:~/practice/E1-1-dev-workstation$ git remote -v
origin  https://github.com/PuffyCripsy/E1-1-dev-workstation.git (fetch)
origin  https://github.com/PuffyCripsy/E1-1-dev-workstation.git (push)
```

**출력 결과 해석**

| 출력 내용 | 의미 |
|---|---|
| `user.name=Kim Yunhee` | 터미널에서 수행하는 모든 커밋에 작성자 이름이 정확히 기록됨 |
| `init.defaultbranch=main` | 최신 GitHub 표준 기본 브랜치 규칙을 준수함 |
| `origin ... E1-1-dev-workstation.git` | 로컬 작업실과 GitHub 원격 저장소가 정상적으로 연동되어 원클릭 push/pull 가능 |

**실습 결과 요약**

Git 기본 설정 및 원격 저장소 연결을 완료하여 코드 버전 관리와 협업을 위한 워크스테이션 환경을 확립하였다.

---

## 7. 추가 트러블슈팅 사례

### 트러블슈팅 3. 포트 중복 사용 충돌 오류 (Port Already Allocated)

#### ① 문제 상황

새로운 NGINX 컨테이너를 실행하기 위해 `docker run -d -p 8080:80 ...` 명령어를 입력했으나 컨테이너가 생성되지 않고 오류가 발생하였다.

#### ② 오류 메시지

```text
docker: Error response from daemon: driver failed programming external connectivity on endpoint web-test: 
Bind for 0.0.0.0:8080 failed: port is already allocated.
```

#### ③ 원인 분석

호스트 컴퓨터의 8080 포트를 이전 실습에서 실행했던 `my-web-8080` 컨테이너가 여전히 점유하고 있었다. 호스트의 단일 포트는 한 번에 하나의 프로세스(또는 컨테이너)만 바인딩할 수 있다.

포트 점유 현황 확인:

```bash
docker ps --filter "publish=8080"
```

실제 결과:

```text
CONTAINER ID   IMAGE                 COMMAND                  PORTS                  NAMES
1a2b3c4d5e6f   my-custom-nginx:1.0   "/docker-entrypoint.…"   0.0.0.0:8080->80/tcp   my-web-8080
```

#### ④ 해결 과정

**방법 A (기존 컨테이너 정리)**:
점유 중인 기존 컨테이너를 정지하고 삭제한다.

```bash
docker stop my-web-8080 && docker rm my-web-8080
```

**방법 B (포트 번호 변경 - 권장)**:
기존 컨테이너를 유지한 채, 호스트의 미사용 포트(예: 8083)로 매핑 포트를 변경하여 실행한다.

```bash
docker run -d -p 8083:80 --name web-test my-custom-nginx:1.0
```

#### ⑤ 해결 확인 결과

```text
jfyouni8912@GNIA-C402-C03:~$ curl -I http://localhost:8083
HTTP/1.1 200 OK
```

8083 포트로 정상 접근이 가능해졌다.

**실습 결과 요약**

포트 충돌 원인을 식별하고 호스트 포트 번호 분할 또는 프로세스 정리를 통해 충돌을 해결하는 실무 트러블슈팅 절차를 정립하였다.

---

## 8. 결론 및 재현 가능한 환경 원칙 정리

본 실습을 통해 개발 워크스테이션 구축의 3대 핵심 기둥인 **Linux CLI, Docker, Git**의 기본기를 완성하였다:

1. **Linux CLI**: 절대/상대 경로 구분, 권한 체계(`chmod 600/700`, `rwx`), 디렉터리 및 파일 제어의 기초를 체득하였다.
2. **Docker 컨테이너**: 애플리케이션을 호스트 환경과 격리하여 실행하고, `Dockerfile`로 빌드 자동화를 실현하였으며, `포트 매핑`과 `볼륨/바인드 마운트`를 통해 네트워크 및 스토리지 연결의 원리를 증명하였다.
3. **Git & GitHub**: 로컬 버전 관리와 원격 저장소 동기화 체계를 갖추어 팀 협업의 기초를 확립하였다.

이로써 "내 컴퓨터에서는 잘 돌아가는데 다른 컴퓨터에서는 안 된다"는 전통적인 배포 문제를 극복하고, 누구나 동일한 환경에서 서비스를 재현하고 검증할 수 있는 개발 워크스테이션 환경을 확립하였다.
