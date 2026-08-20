# AI プロンプト：API 設計生成

## 使用場面

要件ドキュメントとデータモデルから、API 設計を生成します。

## 入力（使用前に記入）

```
要件ドキュメントのパス：docs/REQUIREMENTS.md
データモデル：（貼り付けまたは参照）
認証方式：OA Session / JWT / API Key
統一レスポンス形式：{ code, data, message }
```

## プロンプト

```
ai-engineering-playbook/05-templates/detailed-design-template.md の「API」部分を参照し、
以下の要件ドキュメントとデータモデルに基づいて、完全な API 設計を作成してください。

【要件ドキュメント】
（docs/REQUIREMENTS.md の関連箇所を貼り付け/参照）

【データモデル】
（データモデルを貼り付け）

【制約】
1. API パスは /api/v1/ をプレフィックスにし、kebab-case の複数形で命名
2. 統一レスポンス形式：{ code: number, data?: T, message?: string }
3. 各 API には必ず明記：メソッド、パス、用途、リクエスト、レスポンス、権限要求
4. 境界ケースとエラー応答をすべて列挙
5. 認証が必要な API、アクセス可能な役割を明記

【出力形式】
1. API 一覧表
2. 各 API の詳細定義（リクエスト/レスポンス例、権限、境界ケース）
3. 権限マトリクス
```

## 出力受け入れ

`04-ai-workflows/acceptance-checklists/design-checklist.md` で確認してください。
詳細設計まで一気に書く場合は `output-contracts/detailed-design-output.md` の章立てに従う。
