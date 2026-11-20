---
title: "演習 4 - エージェントの監視と管理"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

これまでの演習では、ユーザー体験の改善や機能追加を目的に、Copilot cloud agent に 3 つの別々のタスクを依頼しました。cloud agent は非同期かつ自律的に動作しますが、タスクの進行状況を監視することも大切です。

GitHub.com の[agents ページ][agents-page]など、cloud agent に割り当てたタスクを管理する方法はいくつかあります。この mission control では、オープンなプル リクエスト (PR) があるエージェント タスクを確認できます。作業内容を調べたり、実行中のセッションに指示を追加したりできます。

このレッスンでは、次のことを行います。

- agents ページで cloud agent のタスクを監視します。
- 実行中のセッションに追加機能を依頼します。

## シナリオ

ハイ コントラスト モードを作成するようエージェントに依頼した後、チームはライト モードも追加したいと考えました。サイトのスタイルと切り替え機能をすでに更新しているため、同じ作業に含めるのが自然です。エージェントにライト モードも追加するよう指示します。

## Copilot cloud agent のタスクを確認する

Copilot cloud agent に割り当てたすべてのタスクの状態を確認します。

1. [Copilot agents ページ](https://github.com/copilot/agents)に移動します。
2. メイン ペインと左ペインのタスク一覧を確認します。コードベースのドキュメント更新、ゲームを変更するアプリケーション プログラミング インターフェイス (API) の生成、Web サイトへのハイ コントラスト モード追加など、Copilot に割り当てたタスクが表示されます。
3. 実行中のタスクを選択し、Copilot が行った操作を確認します。リポジトリのチェックアウト、作業環境の作成、Model Context Protocol (MCP) サーバーの設定、タスクの完了に向けた各種操作などが含まれます。

> [!NOTE]
> 表示される手順は、Copilot の進行状況や作業方法によって異なります。

4. 右側に表示されるプル リクエスト (PR) ペインも確認します。PR と変更されたファイルを確認できます。

## cloud agent に追加の指示を出す

実行中のタスクを確認できたので、ハイ コントラスト モードに取り組んでいる Copilot に、ライト モードの切り替えも追加するよう依頼します。

1. ハイ コントラスト モードのセッションを選択します。正確なタイトルは、Copilot が付けた名前や作業状況によって異なります。

   ![mission control の Accessibility セッション](../../../_images/ex6-accessibility-session.png)

2. セッションがセットアップを終えて作業を始めるまで数分待ちます。次のようなメッセージが表示されたら作業開始です。
3. **Steer active session while Copilot is working** ダイアログに次のプロンプトを入力します。

   ```plaintext
   While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
   ```

   ![agents ページの cloud agent タスク。作業中のセッションに指示を出すダイアログを表示](../../../_images/ex6-steer-cloud-agent-task.png)

4. <kbd>Enter</kbd> を押してプロンプトを送信します。
5. Copilot がプロンプトを受け取り、作業に組み込むことを確認します。

## Copilot の作業を待つ

前と同じように、Copilot は更新されたタスクに取り組みます。メッセージを送った時点で作業中だった手順を終えた後、新しい依頼をワークフローに加えます。

完了まで数分かかります。その間に、ここまでに学んだことを振り返ってください。

## まとめと次のステップ

Copilot agents ページを確認しました。ここは GitHub Copilot cloud agent のタスクを監視して指示するための中心的な場所です。すべての実行中・完了済みタスクを追跡し、作業内容をレビューして、進行中のタスクに指示を追加できます。

このレッスンでは、次のことを行いました。

- mission control と agents ページを使って cloud agent のタスクを監視しました。
- 実行中のセッションに追加機能を依頼しました。

Copilot がアクセシビリティ機能を完成させたら、次は Copilot が作成した[プル リクエストを反復して改善します][next-lesson]。

## リソース

- [Copilot agents ページ][agents-page]
- [カスタム エージェントについて][custom-agents]

---

| [← 前のレッスン: カスタム エージェント][previous-lesson] | [次のレッスン: Copilot の作業を反復する →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
