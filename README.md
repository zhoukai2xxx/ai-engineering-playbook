# AI Engineering Playbook

社内の AI 併用開発のための標準（プレイブック）リポジトリです。プロジェクトの立ち上げから設計・実装・デプロイまでの全工程を規定し、Cursor / AI がそのまま使えるテンプレート、プロンプト、受け入れチェックリストを提供します。

> **初めての方**：[全体説明（日本語）](docs/AI開発標準_全体説明.md) · [全体说明（中文）](docs/AI开发标准_全体说明.md) — リポジトリを clone しなくても読める概要です。

## 用途

- **人が読む**：統一された開発フロー、設計ルール、命名規則
- **AI に使う**：プロンプトのひな形、出力形式の契約、受け入れチェックリスト
- **各プロジェクトで使う**：新規プロジェクト立ち上げ時にテンプレートを複製して標準に沿って進める

## リポジトリ構造

```
ai-engineering-playbook/
├── 00-governance/           # ガバナンス：開発方針、AI 協業ルール
├── 01-project-lifecycle/    # プロジェクトライフサイクル各段階の説明
├── 02-architecture/         # アーキテクチャ規約（フロント/バック/DB/認証）
├── 03-engineering-standards/ # 工学スタンダード（命名/API/Git/Review）
├── 04-ai-workflows/         # AI ワークフロー（プロンプト/出力契約/受け入れ）
├── 05-templates/            # そのまま使えるドキュメントテンプレート
├── 06-reference-projects/   # 参考プロジェクトからの学び（回収）
└── 07-assets/               # 図、例
```

## コア 5 点（毎回使う）

- 最短ガイド：[00-governance/core-five.md](00-governance/core-five.md)

| | 内容 | ファイル |
|--|------|----------|
| A | AI 協業原則（Ask/Agent、人の確認） | [00-governance/ai-collaboration-policy.md](00-governance/ai-collaboration-policy.md) |
| B | タスクカード | [04-ai-workflows/task-templates/](04-ai-workflows/task-templates/) |
| C | 出力契約 | [04-ai-workflows/output-contracts/](04-ai-workflows/output-contracts/) |
| D | プロジェクト立ち上げ | [05-templates/project-kickoff-template.md](05-templates/project-kickoff-template.md) |
| E | 学びの回収 | [06-reference-projects/README.md](06-reference-projects/README.md) |

## クイックスタート：新規プロジェクトの立ち上げ

```
1. project-kickoff-template.md を docs/KICKOFF.md に複製して記入
2. requirements-template.md で要件を書く（prompts/requirements で初稿可）
3. 人が KICKOFF と REQUIREMENTS を確認
4. prompts/design と output-contracts で基本設計/詳細設計/API/DB 草案
5. acceptance-checklists で受け入れ（通らなければ次へ進まない）
6. task-breakdown-prompt + タスクカードで Phase を分解
7. Ask で方針 → 許可があれば Agent で実装
8. 開発中に 06-reference-projects/<project>/ へ学びを追記
```

## 関連リポジトリ

| リポジトリ | 用途 |
|------|------|
| `company-databases` | 各プロジェクトの DB スキーマを統一管理 |
| `interview-management` | 本スタンダードに従って作った最初のプロジェクト（参考） |
| `employee-info-management` | OA システム（既存。徐々に標準へ寄せる） |

## AI 協業原則（要約）

詳細は [00-governance/ai-collaboration-policy.md](00-governance/ai-collaboration-policy.md) を参照してください。

- AI が下書きを作成し、人が確認して実行する
- 各 AI タスクは固定の入力/出力形式と受け入れ基準を持つ
- DB スキーマ変更、権限モデル、プロダクション設定は必ず人が審査する
- 開発中に学びを本リポジトリへ継続回収する
