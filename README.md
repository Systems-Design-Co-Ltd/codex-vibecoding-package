# codex-vibecoding-package

> [!NOTE]
>
>このリポジトリはcodexを使ったAI駆動開発の初期設定ツールを提供します。

## プロジェクト概要

VibeCoding 互換の codex エージェントを構築するためのツールキットとプレイブックです。
このリポジトリは、LLM制御のための共有ガイドライン（`AGENTS.md`）、実行計画（`PLANS.md`）、および将来の SDK ソースコードをホストしています。

## リポジトリレイアウト

- `AGENTS.md`: すべての貢献者向けの基本ルール。
- `PLANS.md`: 正規の ExecPlan テンプレートと作業ログ。
- `docs/`: サポートドキュメント（要件、計画スナップショット、変更履歴など）。

プロジェクトが成長するにつれて、製品コードを `src/` に、プロンプトを `assets/` に、
共有ヘルパーを `src/lib/` に、CI やワークフローファイルを `.github/` に追加します。

## クイックスタート

```bash
pnpm install
pnpm dev --filter codex-vibecoding-package
pnpm build
pnpm test
pnpm lint
```

`.nvmrc` の Node バージョンを使用してリポジトリルートからコマンドを実行します。
外部 API に触れる前に `.env.local` を準備し、キャッシュが誤動作する場合は
pnpm ストアをプルーン（`pnpm store prune`）してください。

**コミット前:** `pnpm lint && pnpm typecheck && pnpm test` を実行してください。
すべての PR で `pnpm build` と一緒に結果を共有してください。

## 作業上の合意事項

- TypeScript strict モード、prettier/eslint のデフォルト、Conventional Commit メッセージに従ってください。
- リスクのある作業には機能フラグ（`config/feature-toggles.json`）を優先してください。
- すべての機能で `docs/changelog.md` と関連する要件ドキュメントを更新してください。
- 参照順序: 最新チャット > カレントディレクトリの `AGENTS.md` > ルート `AGENTS.md` > その他のドキュメント。

## AGENTS.md 作成チートシート

1. **概要 (1-3 行)**: リポジトリが何をするのかを説明する。
2. **構成**: 起点・重要フォルダ・ディレクトリレイアウトを列挙する。
3. **環境のヒント**: パッケージマネージャー、ビルドツール、IDE の癖を説明する。
4. **いつ PLANS.md を使うか**: しきい値を設ける（2ステップ、30分、2人以上など）。
5. **セットアップ/テスト**: 最小限の説明で `pnpm install && pnpm test` のようなコマンドを記載する。
6. **コーディング規約**: リンター、フォーマッター、命名規則、PR ルール。
7. **ポリシー/セーフティレール**: Feature Flag、シークレット管理、レビュー要件。
8. **検証/CI ゲート**: テスト、型チェック、ビルドのしきい値。
9. **禁止事項**: `node_modules` の手動編集、秘密情報のコミット、テストのスキップ。
10. **優先順位/判断基準**: 競合する指示の順位付け。

小規模なリポジトリでもこのフォーマットに従いますが、小さなセクションに凝縮します。
`docs/requirements/` が成長したら参照をリンクするようにしてください。

## PLANS.md / ExecPlan 作成フロー

1. **トリガー**: 作業が 2 ステップを超えるか、30 分を超える、または 2 人以上が関与する。
2. **計画を書く**: 概要、現状、目標、マイルストーン、ステップ、受入基準を埋める。
3. **フィードバック**: ExecPlan を貼り付けてレビュー依頼し、欠落しているリスクや項目について尋ねる。
4. **実行**: 各マイルストーンに取り組み、`PLANS.md` で [完了], [進行中], [保留] を更新する。
5. **継続性**: 発見事項、決定事項、未解決の問題をインラインで記録し、次のエージェント（または自分自身）がコンテキストを失わないようにする。

プロンプトのスケルトンは `assets/prompts/execplan-skeleton.md` を参照してください。
ビルドの進化に合わせて書き込み、読み取り、更新、リンクを行ってください。

## 次のステップ

- **新規メンバー**: `AGENTS.md` を読む → `pnpm install && pnpm test` を実行する → `docs/requirements/` を確認する。
- **貢献者**: 2 ステップを超える作業では ExecPlan を開始する。PR には lint/test の結果を含める。
- **メンテナー**: `AGENTS.md` と `PLANS.md` を同期させ、新しいベストプラクティスが出現したら更新する。

---
**目的**: AI エージェントが迷わず、他の VibeCoding パッケージと一貫性を保ちながらコードを生成できるようにする。
ドキュメントを更新することで、すべてのチームメンバーを支援します。

## 参照すべきサイト
https://cookbook.openai.com/articles/codex_exec_plans
https://qiita.com/masakinihirota/items/8729facb86baa57116f7
https://qiita.com/masakinihirota/items/62367ca7ab1766cbd012
