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
- `-l`: Long
