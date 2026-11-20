---
title: "演習 2 - Copilot Agent Mode で機能を追加する"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

簡単なアプリケーションの変更でも、通常は複数のファイルを更新し、テストを実行する必要があります。開発者は、関連ファイルを探し、変更を行い、テストを実行し、デバッグし、更新し忘れたファイルを見つけて、さらに変更を加えます。この作業は何度も繰り返されることがあります。

Copilot Agent Mode は、統合開発環境 (IDE) 内でより自律的に作業するための機能です。開発者と同様に、プロジェクト構成を調べ、必要なファイルを更新し、テストなどのタスクを実行して、問題があれば自動的に修正します。Agent Mode を使ってサイトに機能を追加します。

> [!NOTE]
> 名前は似ていますが、agent mode と cloud agent は異なる利用体験を提供します。agent mode は IDE 内で動作するため、すばやいフィードバックと対話が可能です。cloud agent はチームの一員のように非同期で作業し、Issue とプル リクエストを通じてやり取りします。

この演習では、次の方法を学びます。

- Copilot Agent Mode でプロジェクトを調べ、関連ファイルを特定し、複数のファイルを連携して変更する。
- ユーザー インターフェイス (UI) とデータ層にまたがる機能を実装する。
- コードベースにマージする前に、Copilot Agent Mode が生成した変更とテストをレビューする。

## シナリオ

ゲームの一覧が増えてきたため、利用者がカテゴリとパブリッシャーで絞り込めるようにします。前の演習では publishers ヘルパーを追加しました。次は Copilot Agent Mode を使い、残りのデータ層、UI、テストを完成させます。

## Tailspin Toys の Web サイトを実行する

変更を加える前に、Tailspin Toys の現在の機能を確認します。

この Web サイトは、開発者をテーマにしたボードゲームのクラウドファンディング プラットフォームです。ゲーム一覧と各ゲームの詳細を表示します。サイトは Astro アプリケーション 1 つで構成され、ビルド時に静的 HyperText Markup Language (HTML) を生成します。ページは Drizzle オブジェクト リレーショナル マッパー (ORM) を介してローカル SQLite データベースを直接照会します。別のバックエンド アプリケーション プログラミング インターフェイス (API) やクライアント側 UI フレームワークはありません。再利用可能なデータ アクセス ヘルパーは `src/lib/` にあり、インタラクティブな動作には Astro の `<script>` と標準 DOM API を使います。

### Web サイトを起動する

`npm run dev` タスクを使うと、GitHub Codespace で Astro の開発サーバーを起動できます。

1. Codespace に戻ります。前の演習の後に `main` に戻っているはずです。
2. Codespace 内で <kbd>Control</kbd>+<kbd>`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux) を押して、新しいターミナルを開きます。
3. 絞り込み作業用のブランチを作成して切り替えます。

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. 次のコマンドで Web サイトを起動します。

   ```bash
   npm run dev
   ```

   Astro の開発サーバーが起動すると、次のような URL を含むメッセージが表示されます。

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> `http://localhost:4321` を開くよう促すダイアログが表示された場合は、**x** を選択して閉じます。

5. ターミナルに表示された `http://localhost:4321` を、<kbd>Command</kbd> (Mac) または <kbd>Ctrl</kbd> (Windows/Linux) を押しながら選択して、Web サイトを開きます。

> [!NOTE]
> Codespace のターミナルから localhost URL を選択すると、`https://<your-codespace-name>-4321.app.github.dev/` に自動的に転送されます。これは Codespace 上の開発サーバーに接続するプライベート トンネルです。

### Web サイトを確認する

Web サイトを起動したら、現在の機能を確認します。

- **ホーム ページ**: タイトル、画像、説明を含むボード ゲームの一覧を表示します。
- **ゲーム詳細ページ**: ゲームを選択すると、タイトル、説明、パブリッシャー、カテゴリなどの情報を表示します。

## Copilot でバックログを確認する

> [!TIP]
> **Copilot Chat を開く**
>
> 次の作業を始める前に、Codespace に戻って Copilot Chat パネルを開き、**New Chat** を選択して新しい会話を始めます。モードとモデルの選択は演習ごとに異なります。必要な場合は、各手順で説明します。

最初の Web サイトは動作していますが、さらに機能を追加します。テンプレートからプロジェクトを作成したときに、Issue のバックログも自動的に作成されています。Copilot に一覧を表示させます。

1. Chat ビューのエージェント ドロップダウンから **Agent** を選びます。Agent は自律的に計画し、複数ファイルを変更し、ターミナル コマンドを実行して、ツールを呼び出します。

   ![Chat ビューのエージェント選択メニュー](../../../_images/shared-chat-mode-selector.png)

2. 利用可能なモデル一覧から **Claude Sonnet 4.5** を選択します。

> [!CAUTION]
> このワークショップは、特定のモデルを推奨するものではありません。作成時に Claude Sonnet 4.5 を使用したため、出力の一貫性を高める目的で手順に記載しています。大規模言語モデル (LLM) は確率的に動作するため、提案は例と異なる場合があります。これは通常の動作です。

> [!NOTE]
> 確率的な動作により、Copilot が異なる Model Context Protocol (MCP) コマンドを使う場合がありますが、タスクは完了できるはずです。

3. 次のプロンプトを Copilot に送り、バックログを確認します。

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. すべての Issue を一覧表示するコマンドを実行するよう求められたら、**Continue** を選択します。
5. 生成された Issue の一覧を確認します。

Copilot が利用者にとって有益だと判断した順に、項目を優先順位付けしたことを確認します。

## 命令ファイルを確認する

コード生成をエージェントに依頼する前に、コンテキストを与える命令ファイルを確認します。Web サイトの機能追加方法に関するガイダンスを含む [user interface (UI)][ui-instructions] ファイルを使います。

1. Codespace で `.github/instructions/ui.instructions.md` に移動します。
2. 機能追加に関する全体的なガイダンスを確認します。アーキテクチャの概要、コンポーネント設計、テスト容易性とアクセシビリティの原則、Astro、Tailwind CSS (Cascading Style Sheets)、Drizzle などのファイル種別に関する命令へのリンクが含まれます。

> [!TIP]
> 命令ファイルから、他の命令ファイルやプロジェクト内のファイルを参照できます。パスは命令ファイルからの相対パスです。命令を再利用し、大きな命令セットを管理しやすく分割して、Copilot に例やテンプレートを示せます。

## 絞り込み機能を実装する

絞り込み機能を完成させるには、少なくとも次の 3 つを更新する必要があります。

- データ層 (`src/lib/`) に残りの絞り込みロジックを追加または改善する。
- 絞り込みの動作を確認するテストを追加または更新する。
- ゲーム一覧ページに絞り込み UI を追加する。

さらに、コードベースにマージする前にテストを実行し、成功させる必要があります。Copilot Agent Mode にこれらの作業を依頼します。

1. 現在の Copilot 会話を続けるか、**New Chat** を選択して新しい会話を始めます。
2. **Add Context**、**Instructions**、**ui** の順に選択し、命令ファイルを追加します。

   ![UI 命令ファイルの選択例](../../../_images/ex3-select-instructions-file.png)

3. Chat ビューのエージェント ドロップダウンで **Agent** が選択されていることを確認します。

   ![Chat ビューのエージェント選択メニュー](../../../_images/shared-chat-mode-selector.png)

4. モデルが **Claude Sonnet 4.5** のままであることを確認します。
5. バックログの関連 Issue に基づいて機能を実装するよう、次のプロンプトを送ります。

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. Copilot がプロジェクトを調べ、機能に関係するデータ層、UI、テストのファイルを探して、変更とテストを始める様子を確認します。

   ![Copilot がプロジェクト ファイルを調べる画面](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot はプロジェクトを調べ、ファイルを変更し、テストを実行します。タスクやコードベースによって数分かかることがあります。作業中、エディターに **Keep** と **Undo** が表示される場合があります。作業中に選択する必要はありません。完了すると、変更ごとに **Keep** または **Undo** が表示されます。

7. Copilot から求められたら、**Continue** を選択してテストを実行します。

   ![Copilot Chat でテスト実行の許可を求めるダイアログ](../../../_images/ex3-agent-mode-run-tests.png)

8. 作業中に一時停止したり、テストが失敗したりする場合があります。Copilot はコード生成とテストを繰り返し、エラーがないと判断するまで修正します。

   ![Copilot Agent Mode の完了した Chat セッション](../../../_images/ex3-agent-mode-proposed-changes.png)

9. 生成されたコードに問題がないか確認します。

> [!CAUTION]
> Copilot や他の AI ツールが生成したコードは、必ずレビューしてください。

10. Web サイトを開いているブラウザーに戻り、新機能を試します。
11. 動作とコードを確認したら、Copilot Chat ウィンドウで **Keep** を選択します。

## まとめと次のステップ

GitHub Copilot Agent Mode を使って、Tailspin Toys の Web サイトに機能を追加しました。この演習では、次のことを学びました。

- Copilot Agent Mode で UI とデータ層にまたがる機能を実装する方法。
- Copilot Agent Mode でプロジェクトを調べ、関連ファイルを特定し、連携した変更を行う方法。
- コードベースにマージする前に、Copilot Agent Mode が生成した変更とテストをレビューする方法。

次は、[Playwright MCP サーバーで機能をテストし][next-lesson]、プル リクエストを作成します。

### 追加の演習 — ページネーションを実装する

ゲーム一覧が増えたら、ページネーションが必要になります。この演習で学んだことを使い、Copilot にページネーションを実装するよう依頼します。実装方法やページ サイズを利用者が選べるようにするかなどを検討してください。望む結果に必要なガイダンスをプロンプトで示し、必要に応じて Copilot に変更や追加のコンテキストを依頼します。これは Copilot を使う通常の作業方法です。

## リソース

- [Copilot の ask、edit、agent mode — 機能と使い分け][choose-mode]
- [VS Code の agent mode][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
