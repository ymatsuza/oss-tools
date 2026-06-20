# oss-tools Index Repository Scaffold Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** `ymatsuza1128/oss-tools` を公開 CLI ツール群のインデックスリポジトリとして整備し、最初のコミットを public push する。

**Architecture:** oss-tools 自体はコードを持たない。LICENSE・README・.gitignore の3ファイルのみで構成し、各ツール（独立 repo）への玄関口となる。spec ドキュメントも同リポジトリに含める。

**Tech Stack:** Markdown, MIT License, Git / GitHub (`gh` CLI)

---

### Task 1: .gitignore を作成する

**Files:**
- Create: `.gitignore`

- [ ] **Step 1: .gitignore を作成する**

`C:\Users\ymats\oss-tools\.gitignore` を以下の内容で作成:

```
# Python
__pycache__/
*.py[cod]
.venv/
*.egg-info/
dist/
build/

# uv
.python-version

# Editor
.vscode/
.idea/
*.swp

# OS
.DS_Store
Thumbs.db
```

- [ ] **Step 2: git status で確認**

```powershell
cd C:\Users\ymats\oss-tools
git status
```

期待出力: `.gitignore` が Untracked files に表示される。

---

### Task 2: LICENSE（MIT）を作成する

**Files:**
- Create: `LICENSE`

- [ ] **Step 1: LICENSE ファイルを作成する**

`C:\Users\ymats\oss-tools\LICENSE` を以下の内容で作成（著者名・年は固定）:

```
MIT License

Copyright (c) 2026 ymatsuza1128

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

- [ ] **Step 2: git status で確認**

```powershell
git status
```

期待出力: `LICENSE` が Untracked files に表示される。

---

### Task 3: README.md（インデックス）を作成する

**Files:**
- Create: `README.md`

- [ ] **Step 1: README.md を作成する**

`C:\Users\ymats\oss-tools\README.md` を以下の内容で作成:

```markdown
# oss-tools

A collection of small, focused CLI tools for everyday developer workflows.
Each tool lives in its own repository — install only what you need.

## Tools

| Tool | Description | Install |
|------|-------------|---------|
| *(first tool coming soon)* | | |

## Installation

Each tool is published to PyPI and can be installed with [uv](https://docs.astral.sh/uv/) or [pipx](https://pipx.pypa.io/):

```bash
uvx <name>                  # run without installing
uv tool install <name>      # install as a persistent tool
pipx install <name>         # alternative
```

Or install directly from GitHub:

```bash
uv tool install "git+https://github.com/ymatsuza1128/<name>.git"
```

## Tool conventions

Each tool in this collection follows the same structure:

- **Language:** Python 3.11
- **Package manager:** [uv](https://docs.astral.sh/uv/)
- **CLI framework:** [Typer](https://typer.tiangolo.com/)
- **Testing:** pytest
- **Architecture:** pure-core logic + thin CLI layer
- **License:** MIT

## License

MIT — see [LICENSE](LICENSE).
```

- [ ] **Step 2: git status で確認**

```powershell
git status
```

期待出力: `README.md` が Untracked files に表示される。

---

### Task 4: spec ドキュメントをステージして最初のコミットを作成する

**Files:**
- Modify: (git staging のみ)

- [ ] **Step 1: 全ファイルをステージする**

```powershell
cd C:\Users\ymats\oss-tools
git add .gitignore LICENSE README.md docs/
```

- [ ] **Step 2: ステージ内容を確認する**

```powershell
git diff --staged --stat
```

期待出力: 4ファイル（`.gitignore`, `LICENSE`, `README.md`, `docs/superpowers/specs/...`, `docs/superpowers/plans/...`）が表示される。

- [ ] **Step 3: コミットする**

```powershell
git -c commit.gpgsign=false commit -m "chore: initial index repository scaffold

Add LICENSE (MIT), README (tool index), .gitignore, and design docs.

Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>"
```

期待出力: `[main (root-commit) xxxxxxx] chore: initial index repository scaffold`

- [ ] **Step 4: コミット内容を確認する**

```powershell
git show --stat HEAD
```

期待出力: 上記ファイル群が `+` で表示される。

---

### Task 5: public push する（要確認）

**Files:**
- なし（git remote 操作のみ）

- [ ] **Step 1: push 前にリモート設定を確認する**

```powershell
git remote -v
```

期待出力:
```
origin  https://github.com/ymatsuza1128/oss-tools.git (fetch)
origin  https://github.com/ymatsuza1128/oss-tools.git (push)
```

- [ ] **Step 2: リポジトリが public であることを確認する（push 前の最終チェック）**

```powershell
gh repo view ymatsuza1128/oss-tools --json visibility -q .visibility
```

期待出力: `PUBLIC`

コミット内容に秘密情報（API キー・個人情報・内部システム名等）が含まれていないことを目視確認してから次のステップへ進む。

- [ ] **Step 3: origin へ push する**

```powershell
git push -u origin main
```

期待出力:
```
Branch 'main' set up to track remote branch 'main' from 'origin'.
```

- [ ] **Step 4: GitHub でリポジトリを確認する**

```powershell
gh repo view ymatsuza1128/oss-tools --web
```

ブラウザで README が表示され、ファイル一覧が揃っていることを確認する。

---

## 完了後にやること

- `HANDOFF-cli-history.md` に従い、[84] CLI履歴/メモ化ツールの開発を別 brainstorming で開始する。
- ツール完成後、このリポジトリの `README.md` のツール一覧テーブルに行を追加して push する。
