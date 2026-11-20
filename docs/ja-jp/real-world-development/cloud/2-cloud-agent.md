---
title: "演習 2 - GitHub Copilot cloud agent"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: カスタム命令][previous-lesson] |
|:--|

技術的負債に悩む組織は少なくありません。未解決のセキュリティ問題、更新が必要なレガシー コード、実装する時間がなくバックログに残った機能などがあります。GitHub Copilot cloud agent は、コードの更新や機能追加などのタスクを自律的に実行できます。作業が終わると、人間の開発者がレビューできるドラフトのプル リクエスト (PR) を作成します。これにより、時間のかかる作業を委任し、開発者はより大きな課題に集中できます。

この演習では、Copilot cloud agent を使って次のことを行います。

- コード生成環境をカスタマイズします。
- 操作を安全に行う方法を確認します。
- 明確な範囲の Issue が重要であることを確認します。
- Issue を Copilot に割り当てます。

## シナリオ

Tailspin Toys には、解決したい技術的負債があります。最初のサイトを構築した委託先が、ドキュメントを十分に作成していません。まず、アプリケーションのエクスポート関数すべてに TypeScript Documentation (TSDoc) コメントを追加します。

デザイン チームは、ゲームの詳細ページに関連ゲームを表示し、同じカテゴリの別のゲームを見つけられるようにしたいと考えています。完成度の高い実装はまだ必要なく、ユーザー体験 (UX) の受け入れテストに使える状態が目標です。この作業は現在のブロッカーですが、ほかに優先度の高い Issue があります。

どちらも優先順位が下がりやすいタスクであり、Copilot cloud agent に割り当てるのに適しています。cloud agent が非同期で作業している間、開発者は別のタスクに取り組み、後から結果をレビューできます。

## GitHub Copilot cloud agent について

[GitHub Copilot cloud agent][copilot-agents] は、人間の開発者と同様にバックグラウンドでタスクを実行できます。たとえば、[GitHub Issue を Copilot に割り当てる][assign-issue]ことができます。割り当てると、Copilot は進行状況を追跡するドラフト PR を作成し、環境を準備して作業を開始します。作業中も完了後もセッションを確認できます。提案された解決策のレビュー準備ができると、プル リクエストで開発者に通知します。

## 範囲が明確な命令の重要性

GitHub Copilot に魔法はありません。考える作業を省略できるわけではありません。一見簡単な操作にも複雑な側面があるため、[cloud agent に依頼するタスクの範囲を慎重に決めてください][cloud-agent-best-practices]。AI ペア プログラマーとして扱い、段階的に作業し、学び、試し、調整します。生成 AI を導入しても、ソフトウェア開発の基本は変わりません。

## このリポジトリのカスタム命令

前の演習では、カスタム命令と Copilot のガイダンスへの反映方法を確認しました。まだ確認していない場合は、ここで `.github/copilot-instructions.md` を読み、コード規約と TSDoc doc comment の要件を確認します。また、`.github/instructions/unit-tests.instructions.md` を開き、`applyTo` frontmatter が `**/*.test.ts` に一致するファイルに命令を適用することを確認します。

次のセクションで `Code lacks documentation` Issue を cloud agent に割り当てます。生成されたプル リクエストで、TSDoc コメント、TypeScript の規約、ファイル コメント ヘッダーを確認してください。これらの内容は命令ファイルから反映されます。後の演習でも、PR のレビュー時に確認します。

## Copilot cloud agent の開発環境を設定する

コードを書くときは、開発環境を準備し、必要なセットアップ スクリプトを実行することがあります。Copilot にタスクを割り当てる場合も同様です。cloud agent はソフトウェア エンジニアのように作業します。

cloud agent は [GitHub Actions][github-actions] を使って作業環境を準備します。`.github/workflows/copilot-setup-steps.yml` に[専用のセットアップ ワークフロー][setup-workflow]を作成すると、作業前に実行するツールや依存関係をカスタマイズできます。このラボ用のワークフローはあらかじめ設定され、Node.js、プロジェクトの依存関係、エンドツーエンド テスト用のブラウザー、単一 Astro アプリ用にマイグレーションとシードを行った SQLite データベースを利用できるようにしています。

```yaml
name: "Copilot Setup Steps"

# リポジトリの「Actions」タブからセットアップ手順をテストできます
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # 手順に必要な最小限のアクセス許可を設定します。Copilot は操作用の独自のトークンを受け取ります
    permissions:
      # 依存関係のインストールなどでセットアップ手順中にリポジトリを複製する場合は、`contents: read` のアクセス許可が必要です。複製しない場合は、手順の完了後に Copilot が自動で行います
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # フロントエンド / アプリのセットアップ - Node.js (アプリ全体は Astro と Drizzle/libSQL で構成されています)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # ビルドとテストでデータを使えるように、ローカルの SQLite データベースをマイグレーションしてシードします
      - name: Set up the database
        run: npm run db:setup
```

GitHub Actions のワークフローと同様の形式ですが、次の点に注意してください。

- `copilot-setup-steps` という 1 つのジョブがあります。このジョブは、Copilot がプル リクエストの作業を始める前に GitHub Actions で実行されます。
- `workflow_dispatch` トリガーがあるため、リポジトリの **Actions** タブからワークフローを手動実行できます。Copilot の実行を待たずに、正常に動くかテストできます。

## ドキュメントを追加する

多くのプロジェクトでは、ドキュメントが古いまま、または不足したままになっています。このような技術的負債は、生産性を下げ、コードベースの保守や新しい開発者の受け入れを難しくします。Copilot はドキュメント作成にも役立つため、このタスクを cloud agent に割り当てます。後の演習で結果をレビューします。

1. 新しいブラウザー タブで github.com のリポジトリを開きます。
2. **Issues** タブを選択します。
3. **New issue** を選択して、新しい Issue のダイアログを開きます。
4. **Blank issue** を選択します。
5. **Title** に `Code lacks documentation` と入力します。
6. **Description** に次の内容を入力します。

   ```plaintext
   Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
   ```

7. **Create** を選択して Issue を作成します。
8. 右側の **Assign to Copilot** を選択して、割り当てダイアログを開きます。

   ![Issue に Copilot を割り当てる画面](../../../_images/shared-assign-copilot.png)

9. **Assign** を選択します。

   ![Copilot の割り当て詳細](../../../_images/ex4-assign-copilot-details.png)

10. **Pull Requests** タブを選択します。
11. 新しく作成されたプル リクエスト (PR) を開きます。タイトルは `[WIP]: Code lacks documentation` のようなものです。一覧に表示されない場合は、少し待ってからブラウザーを更新します。
12. 数分後に、Copilot が TODO リストを作成していることを確認します。

> [!NOTE]
> Copilot の TODO リストが PR に表示されるまで数分かかることがあります。Copilot は前述のワークフローを使って環境を作成し、プロジェクトを分析して、問題への最適な取り組み方を判断しています。

13. TODO リストを読み、Copilot が実行するタスクを確認します。
14. プル リクエストのタイムラインを下にスクロールし、Copilot が Issue の作業を開始したことを示す更新を探します。
15. **View session** ボタンを選択します。

   ![Copilot セッションを表示する画面](../../../_images/ex4-view-session.png)

> [!CAUTION]
> 更新された状態が表示されない場合は、ブラウザーを更新してください。

16. ライブ セッションをスクロールし、Copilot がコードを調べ、現状を把握し、計画を考え、コードを作成する様子を確認します。

作業には数分かかることがあります。cloud agent の利点は非同期で作業できることです。別の作業に取り組むため、次は cloud agent に別のタスクを割り当ててから、アプリケーションの機能開発に移ります。

## ゲーム詳細ページに関連ゲームを追加する

Copilot cloud agent を使うと、開発者がある作業に取り組む間に、別の作業をエージェントに任せられます。デザイン チーム向けの関連ゲーム機能はそれほど時間がかからないかもしれませんが、その時間をほかの作業に使えます。cloud agent に割り当ててみましょう。

1. github.com のリポジトリに戻ります。
2. **Issues** タブを選択します。
3. **New issue** を選択し、新しい Issue のダイアログを開きます。
4. **Blank issue** を選択します。
5. **Title** に `Show related games on the game details page` と入力します。
6. **Description** に次の内容を入力します。

   ```markdown
   We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
   ```

7. **Create** を選択して Issue を作成します。
8. 右側の **Assign to Copilot** を選択して、割り当てダイアログを開きます。

   ![Issue に Copilot を割り当てる画面](../../../_images/shared-assign-copilot.png)

9. **Assign** を選択します。

Issue の最初のコメントに 👀 が表示され、Copilot が作業を始めたことが分かります。

![Copilot が Issue の作業中であることを示す目の絵文字](../../../_images/ex4-issue-eyes-emoji.png)

Copilot は 2 つ目の依頼にも取り組み始めます。cloud agent はソフトウェア エンジニアと同じように動作するため、常に監視する必要はありません。完了後にレビューできます。次は、カスタム エージェントを作成して使います。

## まとめと次のステップ

[GitHub Copilot cloud agent][copilot-agents]を確認しました。cloud agent に Issue を割り当てると、技術的負債の解決、新機能の作成、フレームワーク間のコード移行などを非同期で実行できます。

このレッスンでは、次のことを行いました。

- コード生成環境をカスタマイズしました。
- 操作を安全に行う方法を確認しました。
- 明確な範囲の Issue が重要であることを確認しました。
- Issue を Copilot に割り当てました。

cloud agent がバックグラウンドで作業している間、次はカスタム エージェントを作成して使います。[Copilot cloud agent は Model Context Protocol (MCP) サーバーも利用でき][cloud-agent-mcp]、前のモジュールで確認したカスタム命令にも対応しています。

## リソース

- [Copilot cloud agent について][copilot-agents]
- [GitHub Issue を Copilot に割り当てる][assign-issue]
- [Copilot cloud agent のセットアップ ワークフローのベスト プラクティス][cloud-agent-best-practices]

| [次のレッスン: カスタム エージェント →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
