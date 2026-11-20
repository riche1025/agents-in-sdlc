---
title: "レッスン 12 - GitHub Pages でサイトをデプロイする"
description: "GitHub Copilot app で Pages ワークフローを設定し、プル リクエストをレビューして、公開された Space Quiz を確認します。"
authors:
  - jamesmontemagno
lastUpdated: 2026-10-12
---

Space Quiz を GitHub Pages にデプロイして、誰でもアクセスできるようにします。Copilot はワークフローの準備とデプロイの案内を行いますが、変更をレビューし、サイトが公開されたことを確認するのは開発者です。

このレッスンでは、次のことを行います。

- Copilot に GitHub Pages のデプロイ設定を依頼します。
- ワークフローとプル リクエストをマージ前にレビューします。
- デプロイの進行を確認し、公開されたサイトを検証します。

## シナリオ

Space Quiz は GitHub リポジトリにありますが、まだ誰も簡単に試せる状態ではありません。単一ファイルのサイトを GitHub Pages で公開すれば、サーバーやランタイム依存関係を追加せず、公開 Uniform Resource Locator (URL) からアクセスできるようになります。

## Copilot にデプロイの準備を依頼する

> [!WARNING]
> プル リクエストの作成では、コードがコミットされ、プッシュされることがあります。プロンプトを送る前に、承認設定と送信先リポジトリを確認してください。**すべて承認**が有効な場合、別途確認が求められるとは限りません。

1. `space-quiz` の Copilot app セッションで、次のプロンプトを送信します。

   ```plaintext
   Prepare a GitHub Pages deployment for this repository. Create a GitHub Actions workflow that builds the website if needed and deploys it to GitHub Pages after changes reach the default branch. Add a README describing the app and how to run it locally if one does not already exist. Create a pull request with these changes and report its link and any required Pages settings or permissions. Do not merge, enable auto-merge, change Pages settings, or deploy. Stop and wait for my review.
   ```

## ワークフローとプル リクエストをレビューする

1. README が、リポジトリにまだ存在しない場合にのみ追加されていることを確認します。
2. ワークフローのビルド手順、デプロイ手順、トリガー、権限を含め、プル リクエストの変更をレビューします。
3. ワークフローが、未マージのプル リクエストではなくデフォルト ブランチからデプロイすることを確認します。
4. 修正が必要な場合は依頼し、更新された差分をレビューします。マージを許可する前に、必須のプル リクエスト チェックが成功するまで待ちます。

## マージとデプロイを許可する

> [!WARNING]
> 次のプロンプトを送ると、エージェントによるレビュー済みプル リクエストのマージ、リポジトリの Pages 設定変更、サイト公開を許可することになります。レビューを完了し、リポジトリとプル リクエストを確認してから送信してください。承認設定によっては、再確認なしで操作が実行されます。

1. `<PR_NUMBER>` をレビューしたプル リクエスト番号に置き換え、次のプロンプトを別のメッセージとして送信します。

   ```plaintext
   I have reviewed pull request <PR_NUMBER> in this repository and authorize its merge and deployment. Enable GitHub Pages using GitHub Actions, merge that pull request only after required checks pass, and monitor the deployment until it succeeds. Report the final URL of the live website. If you lack permission to enable Pages or merge, tell me exactly what I need to approve or do; do not report success until the site is live.
   ```

![マージ済みの space-quiz プル リクエスト、Build website、Upload artifact、Deploy to Pages の各ステップが成功した GitHub Actions の Deploy website 実行、および yourname.github.io/space-quiz/ に公開された Space Quiz の 3 段階の図。](../../../_images/first-steps-app-pages-deploy.svg)

## デプロイを確認する

1. GitHub Actions のデプロイ実行を開き、成功するまで確認します。
2. 報告された URL を開き、Space Quiz が表示されることを確認します。

エージェントが Pages の有効化やプル リクエストのマージを行えない場合は、提示された具体的な手順に従います。デプロイが成功し、公開サイトが読み込まれるまでは完了とみなさないでください。

## まとめと次のステップ

Space Quiz を公開し、エージェントの報告だけに頼らず、デプロイを確認しました。続けて、[レッスン 13: レビューと次のステップ][next-lesson]に進みます。

[next-lesson]: ../13-review/
