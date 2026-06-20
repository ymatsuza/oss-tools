# Design: oss-tools 公開インデックスリポジトリ

Date: 2026-06-20

## 概要

`ymatsuza1128/oss-tools` を、CLI ツール群の **公開インデックス** として整備する。
各ツールは独立した public リポジトリ（`ymatsuza1128/<name>`）として管理し、
oss-tools はその玄関口（一覧・install ワンライナー・貢献方法）となる。

## スコープ

**含む（このサイクル）:**
- LICENSE（MIT）
- README.md（ツール索引・install 方法・ツールの型規約）
- .gitignore

**含まない（後続）:**
- 各ツールの実装（[84] CLI履歴/メモ化 等）
- rsed / rcaudit の移設（後で判断）

## oss-tools リポジトリ構成

```
oss-tools/
├─ LICENSE
├─ README.md
└─ .github/
   └─ ISSUE_TEMPLATE/   # 任意・後で追加
```

## 各ツール（独立 repo）の型

リポジトリ: `ymatsuza1128/<name>`（public）

```
<name>/
├─ LICENSE              # MIT
├─ README.md
├─ pyproject.toml       # [project.scripts] でエントリポイント
├─ .python-version      # 3.11
├─ .github/workflows/ci.yml
├─ src/<name>/
│   ├─ core.py          # pure-core（ロジック・IO/CLI非依存）
│   └─ cli.py           # 薄い typer CLI
└─ tests/
```

**スタック:** Python 3.11 / uv / typer / pytest / ruff

**Git 規約:**
- feature → main を `--ff-only` でマージ後ブランチ削除
- `-c commit.gpgsign=false`
- コミット末尾に `Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>` trailer
- commit 後 origin へ自動 push

**install（PyPI 公開後）:**
```bash
uvx <name>
uv tool install <name>
```

**install（GitHub から直接）:**
```bash
uv tool install "git+https://github.com/ymatsuza1128/<name>.git"
```

## 次のアクション

1. oss-tools に LICENSE・README・.gitignore を commit → push（最初の public push は確認する）
2. [84]（CLI履歴/メモ化）を brainstorming → 独立 repo で開発
3. 完成後、oss-tools README のツール一覧に追記
