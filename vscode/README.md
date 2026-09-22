# VS Code

## 설치

| OS | 방법 |
|---|---|
| Windows | https://code.visualstudio.com/ 의 User Installer, 또는 `winget install Microsoft.VisualStudioCode` |
| Ubuntu | https://code.visualstudio.com/docs/setup/linux 의 .deb 다운로드 후 `sudo apt install ./code_*.deb` |

## 파일 위치

| 파일 | Windows | Ubuntu |
|---|---|---|
| `settings.json` | `%APPDATA%\Code\User\settings.json` (= `C:\Users\<사용자>\AppData\Roaming\Code\User\settings.json`) | `~/.config/Code/User/settings.json` |
| `extensions.txt` | 파일이 아니라 설치 목록. 아래 "적용" 명령으로 설치 | 동일 |

VS Code 안에서 열기: `Ctrl+Shift+P` → "Preferences: Open User Settings (JSON)".

## 적용

1. `settings.json`을 위 경로에 복사한다. 기존 파일이 있으면 키 단위로 합친다.
2. 확장 설치
   - bash: `cat extensions.txt | xargs -L 1 code --install-extension`
   - PowerShell: `Get-Content extensions.txt | ForEach-Object { code --install-extension $_ }`
3. VS Code를 열어 테마가 Light 2026이고 터미널 화면만 어두운지 확인한다.

## 메모

- 테마는 Light 2026, 터미널 화면만 Dark 2026 색. `workbench.colorCustomizations` → `[Light 2026]` 블록이 그 역할이다. 색 값은 VS Code 설치 폴더의 `2026-dark.json`과 VS Code 다크 테마용 ANSI 기본값에서 그대로 가져왔다.
- 하단 패널 배경과 우측 터미널 목록은 일부러 밝게 두었다. 패널까지 어둡게 하면 목록에서 터미널을 고를 때 글자가 어두운 배경에 묻혀 안 보였다.
- Claude Code 확장(`anthropic.claude-code`)이 여는 터미널도 이 색을 쓴다. Claude Code 쪽 theme는 `claude-code/`에서 dark로 맞춰 두었다.
- Windows 전용 키 (Ubuntu에서는 빼거나 바꿀 것)
  - `terminal.integrated.defaultProfile.windows`: "Command Prompt". Ubuntu에는 해당 없음.
  - `python.defaultInterpreterPath`: `c:\Users\lsh\anaconda3`. Ubuntu에서는 conda 설치 경로로 바꾼다.
- `editor.defaultFormatter`가 Prettier(`esbenp.prettier-vscode`)로 되어 있지만 확장 목록에는 Prettier가 없다. 적용할 때 사용자에게 Prettier를 설치할지 물을 것.
