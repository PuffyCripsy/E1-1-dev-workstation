# E1-1-dev-workstation
개발 워크스테이션 구축 미션

## Linux 기본 명령어 실습

### 1. 실습 환경

- 운영체제: Windows
- Linux 실행 환경: WSL2 (Windows Subsystem for Linux)
- Linux 배포판: Ubuntu
- 터미널: Ubuntu Bash
- 실습 목적: 디렉터리 생성 및 이동, 파일 생성, 파일 정보 확인

### 2. 디렉터리 및 파일 생성

다음 명령어를 Ubuntu 터미널에서 순서대로 실행한다.

| 순서 | 실행 명령어 | 영어 원어 및 설명 |
|---|---|---|
| 1 | `cd ~` | **Change Directory**: 현재 사용자의 홈 디렉터리로 이동한다. `~`는 홈 디렉터리를 의미한다. |
| 2 | `mkdir practice` | **Make Directory**: 현재 위치에 `practice`라는 새 디렉터리를 생성한다. |
| 3 | `cd practice` | **Change Directory**: 생성한 `practice` 디렉터리 안으로 이동한다. |
| 4 | `touch hello.txt` | **Touch**: `hello.txt`라는 빈 파일을 생성한다. 이미 존재하는 파일이면 접근·수정 시각을 갱신한다. |
| 5 | `ls -l` | **List / Long Listing Format**: 현재 디렉터리의 파일 목록과 권한, 소유자, 크기, 수정 시각 등을 자세히 표시한다. |

**실행 명령어**

```bash
cd ~
mkdir practice
cd practice
touch hello.txt
ls -l
```

**실제 출력 결과**

```text
total 0
-rw-r--r-- 1 user user 0 Nov  5 16:28 hello.txt
```

### 3. 실행 결과 해석

| 출력 항목 | 의미 |
|---|---|
| `total 0` | 표시된 파일들이 사용하는 디스크 블록의 합계 |
| `-rw-r--r--` | 일반 파일이며 소유자는 읽기·쓰기, 그룹과 기타 사용자는 읽기 권한을 가짐 |
| `1` | 하드 링크 수 |
| `user user` | 파일 소유자와 소유 그룹 |
| `0` | 파일 크기 0바이트 |
| `Nov 5 16:28` | 파일의 마지막 수정 시각 |
| `hello.txt` | 생성된 파일 이름 |

### 4. 실습 결과

`mkdir`와 `cd`를 이용하여 실습 디렉터리를 생성하고 이동하였다. `touch`로 빈 텍스트 파일을 생성한 뒤 `ls -l`로 파일의 존재 여부와 접근 권한을 확인하였다.

**실습 증빙**

- 스크린샷 제목: Linux 파일 생성 및 목록 확인
- 파일명: `01_linux_file_creation.png`
- 이미지 링크: 저장소에 스크린샷을 업로드한 뒤 추가 예정

※ 파일 생성 시각과 사용자 이름은 실습 환경에 따라 달라질 수 있다.
