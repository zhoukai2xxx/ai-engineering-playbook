# コア 5 点の使い方

A〜E は毎回の開発で使う最小セット。詳細は各ファイルを正とする。

## A. AI 協業原則

ファイル：`00-governance/ai-collaboration-policy.md`

- AI に任せてよい作業 / 人が必須 / AI が決めてはいけないこと
- Ask と Agent の使い分け
- 先に方案か、直接コードか
- 要件・DB・権限・本番設定の分担例

## B. タスク分解

ファイル：`04-ai-workflows/task-templates/`

- 説明：`README.md`
- 複製用カード：`task-card-template.md`
- 分解プロンプト：`04-ai-workflows/prompts/implementation/task-breakdown-prompt.md`

## C. 出力契約

ファイル：`04-ai-workflows/output-contracts/`

- 一覧：`README.md`
- 詳細設計の章立て：`detailed-design-output.md`

AI への依頼は「書いて」ではなく、契約の章を守らせる。

## D. プロジェクト立ち上げ

ファイル：`05-templates/project-kickoff-template.md`

新規プロジェクトの最初に `docs/KICKOFF.md` へ複製する。以降の AI 会話の共通入力になる。

## E. 学びの回収

ファイル：`06-reference-projects/README.md`

各プロジェクトに `lessons-learned.md` / `adopted-patterns.md` / `mistakes-to-avoid.md` を置く。金曜または Phase 完了時に追記し、有効なものだけプレイブックへ昇格する。
