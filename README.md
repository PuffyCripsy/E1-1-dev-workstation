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
