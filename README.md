# GX Works3 × GitHub Copilot Computer Use — AI Agent PoC

> **非公式・実装前の検討資料（v0.1）**。本リポジトリは GX Works3 を自然言語で操作する PoC の設計・準備資料です。三菱電機の公式プロジェクトではありません。Computer Use による GX Works3 の動作は本リポジトリで検証・保証していません。

## 目的

GX Works3 の習得負担を低減するため、GitHub Copilot の Computer Use を利用して、画面認識・テスト用プロジェクトの新規作成・保存・簡単なラダー編集を自然言語で実行できるか検証します。**オフラインのテスト環境のみ**を対象とし、PLC 実機への接続・書き込み・運転は対象外です。

## まず読む資料

| 資料 | 用途 |
| --- | --- |
| [設計仕様書（Markdown）](docs/spec/GX_Works3_AI_Agent_PoC_Design_Spec_v0.1.md) | 背景・構成・要件・工程・受入基準。Copilot に読ませる本体 |
| [設計仕様書（PDF）](docs/spec/GX_Works3_AI_Agent_PoC_Design_Spec_v0.1.pdf) | 社員への説明・閲覧用 |
| [設計仕様書（Word）](docs/spec/GX_Works3_AI_Agent_PoC_Design_Spec_v0.1.docx) | レビュー・改訂用 |
| [Copilot初回プロンプト](prompts/00_Copilot_Initial_Prompt.md) | 新しいチャットで背景を伝える |
| [Copilot共通指示](.github/copilot-instructions.md) | 操作上のルールと禁止範囲 |
| [操作マニュアル（雛形）](docs/manual/README.md) | 操作手順を整理する入口 |
| [検証プロンプト](prompts/01_inspect_only.md) | 画面読取から段階的に試す |
| [評価記録の雛形](evaluation/experiment_log_template.csv) | 成功・失敗を記録するテンプレート |

## 初期検証の順序

1. 対象GX Works3の版数・CPU機種・Computer Useの利用条件を確認する。
2. VS CodeのローカルGitHub Copilot harnessでComputer Useを有効化する。
3. [画面認識だけ](prompts/01_inspect_only.md)を試し、クリックはさせない。
4. 指定CPU・ラダー言語で新規テストプロジェクトを作成する。
5. 別名で保存し、再オープンして一致を確認する。
6. `docs/manual/` の該当手順をCopilotに明示して再実行する。
7. 成功した操作のみを `.github/skills/` にSkillとして蓄積する。
8. ラダー編集・オフライン検証へ段階的に進む。

## Skillの扱い

- **Computer Use** が実際のGUI操作を行う。Skill自体にマウス操作能力はない。
- **Skill Creator** は、確認済み操作手順をSkill化する際に必要なら導入する外部Skill。まだ同梱していない。
- **awesome-copilot** は外部Skillのカタログ。必須ではない。
- GX Works3用Skillは **実機能確認後** に `.github/skills/gxworks3-basic/SKILL.md` などを作成する。
- 初期段階では独自RAGやMCPサーバーは構築しない。

## Copilotへの最初の指示

VS Codeでこのリポジトリを開いて、新しいCopilotチャットで [設計仕様書（Markdown）](docs/spec/GX_Works3_AI_Agent_PoC_Design_Spec_v0.1.md) と [初回プロンプト](prompts/00_Copilot_Initial_Prompt.md) をコンテキストに加えてください。ファイルが明示的に読まれたことを確認してから進めます。

## 安全と公開範囲

本リポジトリをPublicにする場合は、公開を許可された一般的な検討資料だけを置いてください。社内非公開マニュアル、機器構成、スクリーンショット、実プロジェクト、認証情報、社員情報、検証ログの生データ等は置かないでください。公開可否を担当者に確認してください。Git履歴に入った情報は、後から削除しても複製が残る場合があります。

本リポジトリには、GX Works3の実行プログラム・三菱電機のマニュアル全文・検証済み完成Skillは含まれません。
