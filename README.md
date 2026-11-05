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

