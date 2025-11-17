# AGENTS.mdを作成するコマンドファイル


## 概要
このファイルは、AGENTS.mdを作成するコマンドファイルです。構成とプロジェクトの仕様に基づいて、LLMの挙動を制御するためのルールを作成します。

## AGENTS.mdの基本構成
AGENTS.mdは以下の項目を必ず含むこと。

- プロジェクト概要（１～３行）
- 目的
- いつPLASNS.mdを参照するのか
- プロジェクト構成
- 開発環境のヒント
- セットアップ/ビルド/テスト の手順
- プルリクエストの手順
- コーディング規約/コーディングスタイル
- ガードレール/禁止事項
- 要件・受け入れ基準の参照
- PRルール

**全体構造の階層**

<details>
<summary><strong>Repository Guidelines（ルート）</strong></summary>

<details>
<summary>1. 導入・前提セクション</summary>

- overview（プロジェクト概要）
- Purpose（プロジェクト概要含む）
- ExecPlans / When to Use PLANS.md

</details>

<details>
<summary>2. プロジェクト構造セクション</summary>

- Project Structure & Module Organization
- Dev environment tips（開発環境のヒント）

</details>

<details>
<summary>3. 開発環境セットアップセクション</summary>

- Setup Commands（セットアップコマンド）
- Build, Test, and Development Commands

</details>

<details>
<summary>4. 規約・ルールセクション</summary>

- Repository Conventions
- Coding Style & Naming Conventions & Linter
- Task Policy (Very Important)

</details>

<details>
<summary>5. 開発プロセスセクション</summary>

- Testing Guidelines
- Commit & Pull Request Guidelines（コミット＆プルリクエストの手順）
- Verification

</details>

<details>
<summary>6. リファレンスセクション</summary>

- Files the Agent Should Read First

</details>

<details>
<summary>7. 制約・禁止事項セクション</summary>

- Don'ts

</details>

<details>
<summary>8. その他設定</summary>

- 応答言語設定

</details>