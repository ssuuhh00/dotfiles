# Claude Code statusline

레이트 리밋 진행 막대와 리셋 시각을 보여주는 Claude Code 커스텀 statusline. Claude Code가 새로고침할 때마다 stdin으로 넘겨주는 JSON을 읽어 세 줄로 출력한다.

```
multi-protocol-gateway │ Opus 4.6 │ 74k/1000k

current  ━━━─────────  31%  ⟳ 2:00am
weekly   ────────────   2%  ⟳ apr 10, 9:00pm
```

- 1행: 프로젝트명 │ 모델 │ 컨텍스트 토큰 (사용량/총량)
- 2행: 5시간 레이트 리밋 막대 + 리셋 시각
- 3행: 7일 레이트 리밋 막대 + 리셋 시각
- 사용률에 따라 초록 → 주황 → 노랑 → 빨강

## 설치

스크립트 자체는 설치할 게 없고, OS별로 실행 환경만 갖추면 된다.

| OS | 쓸 파일 | 준비 |
|---|---|---|
| Windows | `statusline-windows.sh` | Git Bash 또는 MSYS2 (bash 4+, GNU date 포함). 추가 설치 없음. `git/` 참고 |
| Ubuntu 24.04 | `statusline-ubuntu.sh` | `sudo apt install -y jq` |
| macOS | `statusline-mac.sh` | `brew install jq` |

세 버전의 출력은 같다. Windows 버전만 jq 없이 grep/sed로 JSON을 읽는다 (Git Bash에는 보통 jq가 없어서).

## 파일 위치

| 파일 | Windows | Ubuntu / macOS |
|---|---|---|
| 스크립트 | `C:\Users\<사용자>\.claude\status-line.sh` | `~/.claude/status-line.sh` |
| 연결 설정 | `C:\Users\<사용자>\.claude\settings.json` 의 `statusLine` | `~/.claude/settings.json` 의 `statusLine` |

파일 이름은 OS와 상관없이 `status-line.sh`로 통일한다. `../settings.json`의 `statusLine.command`가 이 이름을 부른다.

## 적용

1. 자기 OS의 스크립트를 복사하고 실행 권한을 준다.
   ```bash
   cp statusline-windows.sh ~/.claude/status-line.sh   # Ubuntu는 statusline-ubuntu.sh, macOS는 statusline-mac.sh
   chmod +x ~/.claude/status-line.sh
   ```
2. `~/.claude/settings.json`에 아래가 있는지 확인한다. `../settings.json`을 그대로 복사했다면 이미 들어 있다.
   ```json
   "statusLine": {
     "type": "command",
     "command": "bash ~/.claude/status-line.sh",
     "padding": 1
   }
   ```
3. `claude`를 실행해 하단에 세 줄이 뜨는지 본다. 2, 3행은 세션의 첫 API 응답 뒤에야 나타난다.

## 메모

- 레이트 리밋(2, 3행)은 Claude.ai Pro/Max 구독에서만 채워진다. API 키, Bedrock, Vertex 인증에서는 `rate_limits` 객체 자체가 없어 1행만 나온다.
- 데이터 출처: 별도 API 호출이 아니라 Claude Code가 statusline 새로고침마다 stdin으로 JSON을 준다. 쓰는 필드는 `cwd`, `model.display_name`, `context_window.context_window_size`, `context_window.current_usage.*`, `rate_limits.five_hour.*`, `rate_limits.seven_day.*`. 전체 구조와 변경 이력은 [SCHEMA.md](SCHEMA.md).
- Windows 버전 주의: Claude Code가 나중에 `context_window.used_percentage`를 추가하면서, JSON 전체에서 `used_percentage`를 순서대로 긁던 방식이 깨졌다 (첫 번째 값이 레이트 리밋이 아니게 됨). 지금 버전은 `rate_limits` 객체를 먼저 잘라낸 뒤 그 안에서 읽는다. 고칠 때 이 구조를 유지할 것.
- 셸 스크립트는 LF 줄바꿈이어야 한다 (CRLF면 bash가 깨짐). 리포 루트 `.gitattributes`가 `*.sh`를 LF로 고정한다.
- 원래 별도 리포(https://github.com/ssuuhh00/claude-statusline)였던 것을 2026-09-22에 여기로 옮겼다.
