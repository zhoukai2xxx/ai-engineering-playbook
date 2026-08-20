# AI 開発標準 全体説明

> **バージョン**：v0.1（試行版）  
> **最終更新**：2026-08-20  
> **対象**：初めて本標準を知る開発者・プロジェクトリード・レビュアー  
> **本文だけで読める**：リポジトリを clone しなくても、本ファイル単体で全体像を把握できます。詳細テンプレートは末尾のリンクから参照してください。

---

## 1. この標準は何か

**AI Engineering Playbook**（以下「プレイブック」）は、社内の **AI 併用開発の標準** です。

- **人が読むルール**：開発フロー、設計の段階、命名、Git、レビューの考え方
- **AI が使う道具**：プロンプト、出力形式（契約）、受け入れチェックリスト、タスクカード
- **各プロジェクトでの使い方**：テンプレートをプロジェクトの `docs/` に複製し、そこから AI と開発者が同じ前提で作業する

プレイブック自体は **標準を置く倉庫** です。実際のアプリコードは `interview-management` など各プロジェクトのリポジトリに置きます。

**標準リポジトリ**：https://github.com/zhoukai2xxx/ai-engineering-playbook

---

## 2. なぜ必要か

| 課題 | 標準が効く理由 |
|------|----------------|
| 開発者ごとに Cursor の使い方がバラバラ | Ask / Agent の使い分けと「人が確認する境界」を共通にする |
| 要件・設計・実装の受け渡しが曖昧 | KICKOFF → REQUIREMENTS → 設計 → タスク分解の順序を固定する |
| AI 出力の品質が会話次第で変わる | プロンプト・出力契約・チェックリストで入力/出力を固定する |
| 同じ失敗を繰り返す | プロジェクト終了後に学びをプレイブックへ回収する |

**試行の第一号プロジェクト**：`interview-management`（面接管理システム）。プレイブック内の `06-reference-projects/interview-management/` に学びを蓄積しています。

---

## 3. 関連リポジトリとの関係

| リポジトリ | 役割 | 備考 |
|------------|------|------|
| **ai-engineering-playbook** | 開発標準・AI ワークフロー・テンプレート | 本説明の正本 |
| **company-databases** | 各プロジェクトの DB スキーマを統一管理 | プロジェクトごとにディレクトリ分割 |
| **interview-management** 等 | 実際の業務システムのコード | 各システムは独立 Git リポジトリ |
| **employee-info-management** | 既存 OA システム | 段階的に標準へ寄せる |

```
[ ai-engineering-playbook ]  ← 標準・テンプレート・プロンプト
         ↓ 複製・参照
[ 各プロジェクト /docs/ ]    ← KICKOFF, REQUIREMENTS, 設計書
         ↓
[ 各プロジェクトのコード ]    ← 実装
         ↓ スキーマ共有
[ company-databases ]        ← DB 定義の単一の参照先
```

---

## 4. 誰が何を読むか

| 読者 | 最初に読む | 次に読む |
|------|------------|----------|
| **プロジェクトリード** | 本ファイル → [core-five](https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/00-governance/core-five.md) | [AI 協業原則](https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/00-governance/ai-collaboration-policy.md) |
| **開発者** | 本ファイル → [タスクカード](https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/04-ai-workflows/task-templates/task-card-template.md) | 担当 Phase のプロンプト（`04-ai-workflows/prompts/`） |
| **レビュアー** | [受け入れチェックリスト](https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/04-ai-workflows/acceptance-checklists/) | [出力契約](https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/04-ai-workflows/output-contracts/) |

**所要時間の目安**：本ファイル 5〜10 分。実際に手を動かす前に [core-five](https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/00-governance/core-five.md) をさらに 5 分。

---

## 5. 新規プロジェクトの流れ（全体像）

日本の IT で一般的な設計フェーズに沿い、各段階で **AI が下書き → 人が確認** します。

```
プロジェクト立ち上げ (KICKOFF.md)
  ↓
要件定義 (REQUIREMENTS.md)     ← AI 支援 + 人の確認【必須】
  ↓
基本設計 (BASIC-DESIGN.md)     ← AI 支援 + 人の確認
  ↓
詳細設計 (DETAILED-DESIGN.md)  ← API / DB / 画面 + 人の確認
  ↓
環境構築 (SETUP.md)
  ↓
タスク分解（タスクカード）      ← AI 支援
  ↓
各 Phase の実装                 ← Ask で方針 → Agent で実装 + review
  ↓
テスト                          ← AI 支援（ケース/スクリプト）+ 人の確認
  ↓
デプロイ                        ← 人が主導（チェックリストは AI 下書き可）
  ↓
学びの回収 → 06-reference-projects/  ← AI が下書き + 人が選別して登録
```

| フェーズ | 成果物 | テンプレート（プレイブック内） |
|----------|--------|-------------------------------|
| 0 立ち上げ | KICKOFF.md | `05-templates/project-kickoff-template.md` |
| 1 要件 | REQUIREMENTS.md | `05-templates/requirements-template.md` |
| 2 基本設計 | BASIC-DESIGN.md | `05-templates/basic-design-template.md` |
| 3 詳細設計 | DETAILED-DESIGN.md | `05-templates/detailed-design-template.md` |
| 4 環境 | SETUP.md | `05-templates/setup-template.md` |
| 5 実装 | コード | タスクカード + 実装プロンプト |
| 6 テスト | テストケース / テストコード | 受け入れチェックリスト + AI 支援 |
| 7 デプロイ | デプロイ・本番反映 | 人が主導；チェックリストは AI 下書き可 |
| 8 回収 | lessons-learned 等 | `06-reference-projects/`（AI 下書き + 人の選別） |

**受け入れに通らない AI 出力は、次フェーズへ進めません。**

---

## 6. AI（Cursor）の使い方（最低限）

### 6.1 基本原則

1. **AI が下書き、人が決定**：範囲・権限・DB・本番設定は人が確定する  
2. **固定の入力/出力**：場当たりプロンプトではなく、プレイブックのプロンプトと出力契約を使う  
3. **小さく前進**：大きな Phase を一度に任せず、タスクカード単位で進める  
4. **新しい会話の最初**：`docs/KICKOFF.md` と `docs/REQUIREMENTS.md` を AI に読ませる  

### 6.2 Ask と Agent

| モード | 使う場面 |
|--------|----------|
| **Ask** | 方針相談、比較検討、コード理解、review、要件/設計の Markdown 初稿 |
| **Agent** | 設計確定後の実装、ファイル作成/変更、コマンド実行 |

**推奨**：Ask で方針を合意 → タスクカードで範囲を明示 → Agent で実行。

| 判断 | 条件 |
|------|------|
| **先に方案（Ask）** | 新モジュール、権限、DB、外部連携、複数ファイルにまたがる変更 |
| **直接コード（Agent）** | 設計確定済み、変更範囲が明確、1〜2 ファイル程度 |

### 6.3 人の確認が必須

- 要件範囲（何をやる/やらない）
- 権限モデル
- DB スキーマ変更（`company-databases` と整合）
- API 契約の確定
- 本番デプロイ設定・秘密情報
- 外部システム（OA 等）連携方式
- UI/UX の最終判断

### 6.4 AI が直接決めてはいけないこと

- 本番の API Key・パスワード・接続文字列
- データ削除など取り消し不能な操作
- 技術スタックの勝手な変更（プレイブックの標準に従う）
- 既存 OA の中核ロジック変更（明示的な依頼がない限り）

---

## 7. コア 5 点（A〜E）の概要

日常開発で **毎回使う最小セット** です。詳細は各ファイルが正本です。

| | 内容 | プレイブック内の場所 |
|--|------|---------------------|
| **A** | AI 協業原則（Ask/Agent、人の確認境界） | `00-governance/ai-collaboration-policy.md` |
| **B** | タスク分解（タスクカード + 分解プロンプト） | `04-ai-workflows/task-templates/` |
| **C** | 出力契約（AI に守らせる章立て・形式） | `04-ai-workflows/output-contracts/` |
| **D** | プロジェクト立ち上げ（KICKOFF テンプレート） | `05-templates/project-kickoff-template.md` |
| **E** | 学びの回収（lessons / patterns / mistakes） | `06-reference-projects/` |

**覚え方**：A でルールを守り、D でプロジェクトを始め、B+C で AI に任せ、E で次に活かす。

---

## 8. 複数人で開発するとき

| 項目 | ルール |
|------|--------|
| **DB** | スキーマは `company-databases` で共有。変更は指定担当がレビュー後に反映 |
| **タスク** | タスクカード形式を統一（目的・範囲・やらないこと・受け入れ基準） |
| **API / DB 変更** | 人が確定してから実装。AI の草案をそのままマージしない |
| **Git** | `main` は安定。機能は `feature/<phase>-<description>`。commit は `[Phase X] 説明` |
| **ブランチ** | 各自の feature ブランチ → review → マージ |

---

## 9. 技術スタック（標準）

| レイヤ | 第一候補 | 既存プロジェクトの代替 |
|--------|----------|------------------------|
| フルスタック Web | Next.js + TypeScript | — |
| フロント SPA | React + Vite + TypeScript | Bootstrap |
| バックエンド API | Next.js API Routes | Spring Boot（Java） |
| DB | PostgreSQL | — |
| ORM | Prisma | Flyway（Java） |
| スタイル | Tailwind CSS | Bootstrap |
| デプロイ | AWS EC2 + Docker Compose | — |
| AI 支援 | Cursor | — |

新規プロジェクトは原則 **第一候補** を採用します。既存システムは無理に書き換えず、触る部分から標準へ寄せます。

---

## 10. よくある質問

**Q. プレイブックのファイルを全部埋めないとダメ？**  
A. いいえ。**コア 5 点（A〜E）** と、プロジェクトの `docs/KICKOFF.md`・`REQUIREMENTS.md` から始めれば十分です。未作成の章は随時追加します（v0.1 は試行版です）。

**Q. 既存プロジェクトにも使える？**  
A. はい。新機能追加時にタスクカードと AI 協業原則だけ適用する、設計書を後追いで整える、など段階的導入が可能です。

**Q. 日本語だけ？**  
A. プレイブック本体は **日本語** を正本とします。中国語の全体説明は `docs/AI开发标准_全体说明.md` を参照してください。

**Q. このファイルだけ配ってもいい？**  
A. はい。まず全体像を共有し、合意後にプレイブックの URL や clone を案内する運用を想定しています。

**Q. README と何が違う？**  
A. 本ファイルは **初見の人向けの説明** です。README はリポジトリ内の索引、core-five は **作業開始時の最短手順** です。

---

## 11. 次に読むファイル（リンク一覧）

| 用途 | URL |
|------|-----|
| リポジトリ全体 | https://github.com/zhoukai2xxx/ai-engineering-playbook |
| README（索引） | https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/README.md |
| コア 5 点 | https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/00-governance/core-five.md |
| AI 協業原則 | https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/00-governance/ai-collaboration-policy.md |
| 開発総則 | https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/00-governance/development-policy.md |
| ライフサイクル | https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/01-project-lifecycle/README.md |
| タスクカード | https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/04-ai-workflows/task-templates/task-card-template.md |
| 受け入れチェックリスト | https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/04-ai-workflows/acceptance-checklists/ |
| KICKOFF テンプレート | https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/05-templates/project-kickoff-template.md |
| 要件テンプレート | https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/05-templates/requirements-template.md |
| 参考プロジェクト（面接管理） | https://github.com/zhoukai2xxx/ai-engineering-playbook/tree/main/06-reference-projects/interview-management |
| 中国語版全体説明 | https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/docs/AI开发标准_全体说明.md |

---

*本文は AI Engineering Playbook の概要です。テンプレート・プロンプト・チェックリストの最新版は上記リポジトリを正とします。*
