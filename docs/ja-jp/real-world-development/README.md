---
title: "実践的な開発"
slug: ja-jp/real-world-development
authors:
  - geektrainer
lastUpdated: 2026-09-16
---

現実的なシナリオ、完成したアプリケーション、共有バックログを使って、ソフトウェア開発ライフサイクル全体で GitHub Copilot を活用します。変更の計画、コード作成、動作テスト、プル リクエストのレビュー、エージェントを使った作業管理を繰り返し行います。

## シナリオ

開発者をテーマにしたボードゲームのクラウドファンディングを提供する架空企業 Tailspin Toys に、新しい開発者として参加します。チームのバックログは GitHub Issue として用意されています。カテゴリやパブリッシャーによる絞り込みなどの機能開発に加えて、アクセシビリティやコーディング標準の改善にも取り組みます。

## 作業環境を選ぶ

GitHub Copilot は、開発者が作業する場所に合わせて利用できます。自分の開発スタイルに合う環境を選んでください。各ワークショップでは個別のセットアップを行い、共通の Tailspin Toys シナリオに取り組みます。

### [GitHub Copilot CLI][cli]

ターミナルでエージェント型アシスタントを使います。Plan モードと Autopilot モード、命令、スキル、カスタム エージェント、Playwright Model Context Protocol (MCP)、Agent Merge、便利なスラッシュ コマンドを活用します。

### [GitHub Copilot app][app]

デスクトップ アプリでエージェント セッションを並行して実行し、セッション モードを切り替え、Canvas で共同作業し、GitHub Issue とプル リクエストを管理します。

### [GitHub Copilot cloud agent][cloud]

GitHub Issue を非同期エージェントに割り当て、作業の指示や進捗確認を行い、作成されたプル リクエストをレビューします。

### [Visual Studio Code][vscode]

Visual Studio Code と GitHub Codespaces で GitHub Copilot を使用します。エディターを離れずに、Copilot Chat の agent mode、MCP サーバー、カスタム エージェントを活用します。

[cli]: cli/
[app]: app/
[cloud]: cloud/
[vscode]: vscode/
