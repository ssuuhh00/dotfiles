# dotfiles

이수행(ssuuhh00)의 개인 환경 설정 모음. 새 컴퓨터(Windows 또는 Ubuntu)에 프로그램을 설치하고 설정을 옮길 때 쓴다.
사람이 읽어도 되지만, 주 독자는 이 리포를 보고 설정을 대신 적용해 주는 AI 에이전트다.

## 목차

| 폴더 | 무엇 | 상태 |
|---|---|---|
| `vscode/` | VS Code 설정(settings.json), 확장 목록 | 사용 중 (Windows에서 뽑음) |
| `claude-code/` | Claude Code CLI 설정(settings.json), statusline 스크립트(`statusline/`, Windows/Ubuntu/macOS) | 사용 중 |
| `git/` | git 전역 설정(.gitconfig) | 사용 중 |

추가 예정: `terminal/` (Windows Terminal, bash), `chrome/` (확장 목록), `os/windows/`, `os/ubuntu/` (패키지 목록, 폰트, 한글 입력기).

## 에이전트 적용 절차

1. 이 목차를 보고 사용자에게 **어떤 항목을 적용할지** 먼저 묻는다. 전부 적용이 기본이 아니다.
2. 고른 폴더의 `README.md`를 읽는다. 모든 폴더 README는 같은 4단락이다: 설치, 파일 위치, 적용, 메모.
3. "파일 위치" 표에서 현재 OS의 대상 경로를 찾는다.
4. 대상 파일이 이미 있으면 덮어쓰지 말고 차이를 보여 준 뒤 합친다. 없으면 그대로 복사한다.
5. 메모에 "Windows 전용"으로 표시된 키는 Ubuntu에서는 빼거나 그 OS 값으로 바꾼다.
6. 적용 후 프로그램을 열어 반영됐는지 확인하고 결과를 보고한다.

## 규칙

- 비밀값(토큰, 비밀번호, 로그인 정보)은 절대 올리지 않는다. `~/.claude.json`, `~/.claude/.credentials.json`, `~/.git-credentials`는 이 리포 대상이 아니다.
- 그대로 복사해서 쓸 수 있는 원본 파일을 올린다. 설명만 있고 파일이 없는 항목은 만들지 않는다.
- 설정을 바꾸면 이 리포도 같이 갱신하고, 폴더 README의 "메모"에 이유를 한 줄 남긴다.
- 셸 스크립트(`*.sh`)는 LF 줄바꿈. 루트 `.gitattributes`가 강제한다. 하위 프로그램 폴더(예: `claude-code/statusline/`)도 같은 4단락 README를 갖는다.

## 폴더 README 형식

```
# <프로그램>
## 설치        — OS별 설치 명령 또는 링크
## 파일 위치   — 표: 파일 | Windows | Ubuntu
## 적용        — 복사 순서, 확인 방법
## 메모        — 왜 이렇게 했는지, OS 전용 키
```
