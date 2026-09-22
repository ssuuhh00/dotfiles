# git

## 설치

| OS | 방법 |
|---|---|
| Windows | https://git-scm.com/download/win (Git Bash 포함. Claude Code statusline에도 필요) |
| Ubuntu | `sudo apt install -y git` |

GitHub CLI(gh)도 같이 설치한다. Windows `winget install GitHub.cli`, Ubuntu는 https://github.com/cli/cli/blob/trunk/docs/install_linux.md. 설치 후 `gh auth login`.

## 파일 위치

| 파일 | Windows | Ubuntu |
|---|---|---|
| `.gitconfig` | `C:\Users\<사용자>\.gitconfig` | `~/.gitconfig` |

## 적용

1. `.gitconfig`를 위 경로에 복사한다.
2. `git config --global --list`로 user.name, user.email을 확인한다.
3. `gh auth login`으로 GitHub에 로그인한다.

## 메모

- 이메일은 GitHub noreply 주소를 쓴다. 커밋에 실제 이메일이 노출되지 않게 하기 위해서다.
- `credential.helper = store`는 자격 증명을 `~/.git-credentials`에 평문으로 저장한다. 새 컴에서는 Windows의 기본 `manager`나 `gh auth setup-git`을 써도 되고, 그 경우 이 줄은 뺀다.
