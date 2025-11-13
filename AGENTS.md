# Repository Guidelines

## プロジェクト概要（1〜3行）

## プロジェクト構成
以下にプロジェクトの構成を記入します。

記入例：
- `/index.html`: エントリーページ（基本レイアウトと簡易スタイル）
- `/assets/`: 画像・フォント等のアセット（必要に応じて）
- `/styles`: 共有ページ別のCSS（任意）。
- `/scripts`: JavaScriptsモジュール（任意）。

## Dev environment tips: 開発環境のヒント
- `ls`でフォルダをスキャンする代わりに、`pnpm dlx turbo run where <project_name>` を使って特定のパッケージに直接移動してください。
- `pnpm install --filter <project_name>` を実行して、Vite、ESLint、TypeScriptが認識できるように、パッケージをワークスペースに追加してください。
- `pnpm create vite@latest <project_name> -- --template react-ts` を使って、TypeScriptの型チェックが設定済みの新しいReact + Viteパッケージを作成してください。
- 各パッケージのpackage.json内にある`name`フィールドを確認して、正しい名前を把握してください（一番上の階層のものは無視してください）。

## ExecPlans / When to Use PLANS.md: いつPlansを参照するかを規定
複雑な機能や大規模なリファクタリングを実装する際は、設計から実装まで必ず ExecPlan（`./PLANS.md` に記載）を使用してください。

「exec plan」という言葉を使ったときは、
plans.md を参照し、以下を実行してください：

1. 全体像を理解する
2. 進捗状況を確認する
3. 作業後に `plans.md` を更新する
4. 発見事項と決定事項を記録する

plans.md はあなたの長期記憶であり、
プロジェクトの羅針盤です。

（閾値の明文化）
- 実装や調査が 2 ステップ以上になりそうなとき、または 30 分を超える見込みの作業では `PLANS.md` を参照してください。ファイルが無ければ作成し、目的・手順・担当を明記してください。
- ステークホルダーが 2 名以上関与する場合や、ロールアウトを段階化する必要がある場合も作成義務があります。
- 単純なコピー修正や 1 ファイル修正は免除対象ですが、判断に迷ったら作るのが原則です。


## Purpose / Intent（何のための文書か）
この文書は codex-vibecoding-package に貢献する全エージェント開発者向けの実務ガイドです。レポジトリ構造、作業手順、品質基準、優先順位を一望できるようにし、指示の衝突を減らします。新規参加者が 1 スプリント以内に成果を出せるよう、意思決定の背後にある背景も端的に記しています。既存メンバーにとっても、判断が迷いやすいポイントを素早く参照するカタログとして機能します。

## 開発・実行コマンド
ビルドやデプロイの実行コマンドを記載します。

## Repository Context（技術スタック、重要ディレクトリ、エントリポイント）
技術スタックは TypeScript + pnpm + Vitest + ESLint/Prettier。実装の起点は `src/index.ts`（SDK のエクスポート兼 CLI エントリ）で、エージェント別ロジックは `src/agents/<agent-name>/` に置きます。共通ユーティリティは `src/lib/`、共有プロンプトは `assets/prompts/`、テスト補助は `tests/support/`、設定メモは `docs/` 以下に整理してください。CI 設定やテンプレートは `.github/` に入れ、環境変数の型定義は `types/env.d.ts` にまとめます。リリースノートは `docs/changelog.md` を更新し、変更点を他の vibecoding パッケージと同期させます。


## Setup / Run / Test：セットアップ/ビルド/テスト（コマンドを“そのまま実行できる形”で）
```bash
pnpm install
pnpm dev --filter codex-vibecoding-package
pnpm build
pnpm test
pnpm lint
```
各コマンドはリポジトリルートから実行し、CI と同じ Node バージョン（`.nvmrc` 参照）を使います。外部 API 連携を確認する際は `.env.local` を用意し、`pnpm dev` でホットリロードしながら挙動を検証します。キャッシュが壊れた場合は `pnpm store prune` でワークスペースを整えてから再実行してください。

- 依存解決: `pnpm i`
- Lint/Typecheck: `pnpm lint && pnpm typecheck`
- 単体テスト: `pnpm test`
- E2E: `pnpm e2e`
- 変更をコミットする前に上のチェックが**全て緑**であること

### テストの手順
- CI（継続的インテグレーション）の計画は `.github/workflows` フォルダ内にあります。
- `pnpm turbo run test --filter <project_name>` を実行して、そのパッケージに定義されている全てのチェックを実行してください。
- パッケージのルートディレクトリからは、単に `pnpm test` を呼び出すだけでテストが実行できます。マージする前に、コミットが全てのテストに合格している必要があります。
- 特定の一つのステップに集中したい場合は、`pnpm vitest run -t "<test name>"` のようにVitestのパターンを追加してください。
- テストスイート全体が成功（グリーン）になるまで、テストや型のエラーを修正してください。
- ファイルを移動したり、インポート文を変更した後は、`pnpm lint --filter <project_name>` を実行して、ESLintとTypeScriptのルールに違反していないか確認してください。
- 誰かに頼まれなくても、変更したコードに対応するテストを追加または更新してください。

## プルリクエストの手順
- タイトルのフォーマット: `[<project_name>] <タイトル>`
- コミットする前には、必ず `pnpm lint` と `pnpm test` を実行してください。

## Code Style / Conventions：コーディング規約（リンタ、整形、型、コミット規約、命名規則）
- TypeScript: strict。import順序はeslint-plugin-importに従う。PRごとに型エラーゼロ。
- PRタイトル: `[api] 説明…` の形式。
- ESNext 構文の TypeScript を 2 スペース・末尾カンマで統一し、`pnpm lint --fix` で ESLint + Prettier を適用します。型の曖昧さを避けるため `any` は原則禁止、必要時はコメントで理由を明記。
- ディレクトリはケバブケース、変数・関数はキャメルケース、クラスはパスカルケース。
- ドキュメントファイルは 80 文字を目安に改行し、日本語テキストでも記号類は半角で統一します。
- コミットは Conventional Commits を必須とし、本文でテスト結果や背景を補足します。
- TailwindCSSを用いた美しいデザインを作成する。

## Task Policy / Safety Rails（分割、レビュー、Feature Flag、秘密管理）
- 大きな変更は最初に概要 Issue を作り、機能フラグや `config/feature-toggles.json` で段階的に有効化します。
- レビュー前に self-review チェックリスト（lint/test/手動確認）をコメントで残してください。
- 秘密情報は `.env.local` と `process.env.*` を通し、ログには入れないこと。
- サブタスクが複数に分かれるときは実装前に TODO コメントや追跡 Issue を分割し、並列開発時は Feature Flag を必ずデフォルト OFF に保ちます。

## Verification / CI gates（テスト必須・型チェック・ビルド）
- PR には `pnpm test`, `pnpm lint`, `pnpm build` の結果を貼り付け、Vitest のカバレッジ 85% 以上を維持する。
- 型チェックは `pnpm tsc --noEmit` で行い、CI でも同じコマンドを実行する。
- フェイルしたチェックは必ず修正してからレビューを依頼してください。
- 外部サービスに依存するテストはモック化し、統合テストは `CI_E2E=1 pnpm test` のようにフラグで切り替えます。

## Don’ts（やってはいけないことのブラックリスト）
- 手動で `node_modules` を改変しない
- `git rebase -i main` で履歴を書き換えない
- 秘密鍵や `.env*` をコミットしない
- 未検証のプロンプト変更を本番フラグに直結させない。
- 生成 AI の出力を無検証で貼り付けること、未使用コードを放置することも禁止です。
- CI が赤い状態でマージしない、明示的な承認なくサードパーティ依存を追加しないことも厳守します。
- 破壊的な変更は行わない。
- 秘密情報を追加しない。生成コードにAPIキーを埋め込まない。
- ハードコーディングは行わない。

## Priority / Tie-breakers（指示衝突時の優先順位）
指示の優先順は「最新チャット指示 > カレントディレクトリの AGENTS.md > ルート AGENTS.md > リポジトリ既定（README 等）」です。競合する場合は必ず上位の指示に従い、不明点は Issue またはチャットで必ず確認してください。

## 要件・受入基準の参照
- **実装前に**以下を必ず読む：`docs/requirements/README.md`
- 今回の作業対象がある場合、該当機能の文書を開き**受入基準(Acceptance Criteria)**を満たすテストを追加/更新すること。

## PRルール
- 変更理由/影響範囲/テスト結果をPR本文に記載。
