# Claude Code (CLI)

## 설치

| OS | 방법 |
|---|---|
| 공통 | https://code.claude.com/docs 의 설치 안내를 따른다. 설치 후 `claude` 실행 → 브라우저 로그인. |
| Windows | Git Bash가 필요하다 (statusline 스크립트가 bash로 돈다). `git/` 참고. |
| Ubuntu | `sudo apt install -y jq` (statusline Ubuntu 버전이 jq를 쓴다). |

로그인 정보는 `~/.claude/.credentials.json`과 `~/.claude.json`에 저장되며 이 리포에 올리지 않는다.

## 파일 위치

| 파일 | Windows | Ubuntu |
|---|---|---|
| `settings.json` | `C:\Users\<사용자>\.claude\settings.json` | `~/.claude/settings.json` |
| `statusline/statusline-*.sh` (OS에 맞는 것 하나) | `C:\Users\<사용자>\.claude\status-line.sh` | `~/.claude/status-line.sh` |

## 적용

1. `settings.json`을 위 경로에 복사한다.
2. statusline은 `statusline/` 폴더의 README를 따라 자기 OS 스크립트를 `~/.claude/status-line.sh`로 복사하고 실행 권한을 준다. `settings.json`의 `statusLine.command`가 이 이름을 부른다.
3. `claude`를 실행해 하단에 statusline 3줄이 뜨는지, `/theme`이 dark인지 확인한다.

## 메모

- `theme: dark`는 VS Code 터미널 화면을 어둡게 해 두었기 때문이다 (`vscode/` 메모 참고). 터미널이 밝은 환경이면 `auto`로 바꾼다.
- `model`, `effortLevel`, `modelSettings`는 취향. 모델 이름은 시간이 지나면 바뀌니 적용 시점의 최신 이름으로 바꿔도 된다.
- Windows 전용: `permissions.allow`의 `Bash(curl.exe:*)`. Ubuntu에서는 빼도 된다.
- `enabledPlugins`의 frontend-design 플러그인은 새 컴에서 다시 설치해야 할 수 있다.
- 전역 지시문 `~/.claude/CLAUDE.md`는 현재 비어 있어 올리지 않았다.
- statusline 스크립트의 동작 원리와 스키마는 `statusline/README.md`, `statusline/SCHEMA.md`에 있다.
