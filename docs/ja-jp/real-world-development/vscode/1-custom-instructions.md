---
title: "演習 1 - カスタム命令 (VS Code)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: 前提条件][previous-lesson] · [次のレッスン: Agent mode →][next-lesson]

生成 AI を使う際は、コンテキストが重要です。タスクを特定の方法で実行したい場合や、Copilot に知っておいてほしい背景情報がある場合は、そのコンテキストを参照できるようにします。[命令ファイル][instruction-files]を使うと、コード生成に関するガイダンスを伝えられます。

この演習では、次のことを行います。

- リポジトリのカスタム命令とパスに応じた命令ファイルを通じて、プロジェクト固有のコンテキスト、コーディング ガイドライン、ドキュメント標準が Copilot に伝わる方法を確認します。
- 現在の命令を使って、絞り込み用の最初のデータ スライス (publishers ヘルパー) を生成します。
- `.github/copilot-instructions.md` にリポジトリ全体に適用する標準を追加します。
- 同じプロンプトを再実行し、生成コードが新しい標準に従う様子を確認します。
- 命令の更新と絞り込みの基盤を `main` にコミットし、次の演習で新しいガイダンスを使えるようにします。

> [!CAUTION]
> 生成コードが、設定した標準すべてに従うとは限りません。Copilot は確率的に動作します。この演習の目的は、更新後の動作の傾向を確認することであり、出力を一字一句合わせることではありません。

## 命令ファイル

### シナリオ

Tailspin Toys には、開発手法に関するガイドラインがあります。

- データ層には必ずユニット テストを用意します。
- ユーザー インターフェイス (UI) はダーク モードで、現代的な見た目にします。
- コードには TypeScript Documentation (TSDoc) コメントを使ってドキュメントを追加します。
- 各ファイルの先頭に、ファイルの役割を説明するコメント ブロックを追加します。

命令ファイルを使い、Copilot がこれらの開発手法に沿って作業できるようにします。

### カスタム命令

カスタム命令を使うと、コーディング スタイルや要件を Copilot に伝え、より適切な提案やコード スニペットを得られます。リポジトリ全体に適用する命令と、特定のファイル種別に適用する命令を作成できます。

命令ファイルには、次の 2 種類があります。

- `.github/copilot-instructions.md` は、リポジトリに関するすべてのリクエストで Copilot に送られます。技術スタック、構築しているものの概要、ベスト プラクティスなど、プロジェクト全体に関係する情報を記述します。
- `.github/instructions/*.instructions.md` は、TypeScript や Astro などの特定の言語や、UI コンポーネントやユニット テストの作成などのタスクに関するガイドラインを記述します。

> [!NOTE]
> IDE では、命令ファイルは Copilot Chat のコード生成にのみ使われ、コード補完や次の編集候補には使われません。
>
> Copilot Chat、Copilot CLI、Copilot cloud agent は、コード生成時にリポジトリ レベルの命令と `applyTo` frontmatter を持つ `*.instructions.md` ファイルの両方を使います。
>
> Copilot は AGENTS.md や CLAUDE.md など、別の標準による命令ファイルにも対応しています。詳細は[カスタム命令のサポート状況][custom-instructions-support]を参照してください。

### 命令ファイルを管理するためのベスト プラクティス

命令ファイルの作成に関する詳しい説明はこの演習の範囲外ですが、サンプル プロジェクトには代表的な構成例があります。

- `copilot-instructions.md` には、構築しているものの説明、プロジェクト構成、全体的なコーディング標準など、プロジェクト全体のガイダンスを記述します。
- `*.instructions.md` には、ユニット テスト、Astro コンポーネント、データ層などのファイル種別や、特定タスクに関する命令を記述します。
- 自然な言葉を使い、明確なガイダンスとコードの例を示します。

命令ファイルや AI の使い方に唯一の正解はありません。プロジェクトに合う方法は、試行を通じて見つけてください。

> [!TIP]
> GitHub Copilot を使うプロジェクトには、実用的な命令ファイルを用意することをお勧めします。このプロジェクトには、[UI 更新][ui-instructions]や [Astro][astro-instructions]など、さまざまなタスク向けのファイルがあります。
>
> Copilot に命令ファイルを作成させることもできます。VS Code の **Configure Chat → Generate Agent Instructions** や Copilot CLI の `/init` など、環境によって方法が異なります。該当する手順は各ハーネスで説明します。
>
> テンプレートや出発点を探す場合は、命令ファイル、カスタム エージェントなどを集めた [awesome-copilot][awesome-copilot] を確認してください。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## プロジェクトのカスタム命令ファイルを確認する

このリポジトリには、`.github/copilot-instructions.md` と、タスク別の `*.instructions.md` ファイルがあります。エディターまたは GitHub Web UI で開いて確認します。

1. `.github/copilot-instructions.md` を開きます。
2. プロジェクトの概要と **Agent notes**、**Code standards**、**Scripts**、**Repository Structure** などのセクションを確認します。**Code standards** の **GitHub Actions Workflows** のガイダンスも確認してください。
3. `.github/instructions` フォルダーを開き、Astro、Drizzle データ層、テストなどに関する命令を確認します。
4. `.github/instructions/unit-tests.instructions.md` を開き、先頭の `applyTo` フィールドが、リポジトリ ルートからの glob を定義していることを確認します。たとえば `**/*.test.ts` に一致する TypeScript テスト ファイルに適用されます。
5. このプロジェクトでユニット テストを作成するための命令を確認します。
6. `.github/instructions/drizzle.instructions.md` の末尾まで読み、`unit-tests.instructions.md` などの命令ファイルや既存ファイルへのリンクを確認します。パスは命令ファイルからの相対パスです。

> [!NOTE]
> `copilot-instructions.md` の **Code formatting requirements** セクションにはプロジェクトのコーディング標準が記載されていますが、コード内のドキュメント化はまだ必須ではありません。後の手順で TSDoc コメントとファイル ヘッダーの規則を追加します。

## 変更用ブランチを作成する

ベスト プラクティスに沿って、変更用ブランチを作成します。

1. 前の演習で使った Codespace に戻ります。
2. <kbd>Control</kbd>+<kbd>`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux) を押して、新しいターミナルを開きます。
3. ブランチを作成して切り替えます。

   ```bash
   git checkout -b custom-instructions
   ```

## 命令を更新する前に Copilot Chat を使う

> [!TIP]
> **Copilot Chat を開く**
>
> 次の作業を始める前に、Codespace に戻って Copilot Chat パネルを開き、**New Chat** を選択して新しい会話を始めます。モードとモデルの選択は演習ごとに異なります。必要な場合は、各手順で説明します。

カスタム命令の効果を確かめるため、まず現在の命令ファイルを使ってプロンプトを送ります。その後、命令を更新して同じプロンプトを再送します。

1. 前の演習で使ったエディター タブを閉じ、Copilot に渡すコンテキストを絞ります。
2. `src/lib/publishers.ts` を開き、ヘルパーを置く場所を Copilot に示します。
3. Chat ビューのエージェント ドロップダウンから **Agent** を選び、ファイルを変更できるようにします。

   ![Chat ビューのエージェント選択メニュー](../../../_images/shared-chat-mode-selector.png)

4. 次のプロンプトを送ります。

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

5. Copilot がプロジェクトを確認し、ヘルパーとテストなどのファイルを更新する様子を確認します。
6. 提案されたヘルパーが、`db` クライアントを最初の引数に取り、型付きのパブリッシャー配列を返す関数であることを確認します。これは `src/lib/*.ts` に適用される `.github/instructions/drizzle.instructions.md` のデータ層規約によるものです。
7. 提案されたコードに TSDoc コメントとファイル コメント ヘッダーが**ない**ことを確認します。

> [!CAUTION]
> Copilot は確率的に動作するため、命令がなくてもドキュメント コメントを追加することがあります。その場合も問題ありません。この演習では、命令の更新後に一貫性が改善されることを確認します。

## リポジトリ全体に適用する標準を追加する

`.github/copilot-instructions.md` はプロジェクト全体の情報を Copilot に提供します。コード提案の改善に役立つよう、コーディング標準を追加します。

1. `.github/copilot-instructions.md` を開き直します。
2. 27 行目あたりの **Code formatting requirements** セクションを探します。既存の標準を確認します。コード内ドキュメントのルールがまだないことにも注目してください。
3. 既存の標準の直後に、次の内容を追加します。

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. `copilot-instructions.md` を保存します。

> [!TIP]
> リポジトリ全体に適用する `.github/copilot-instructions.md` と、言語、ファイル種別、タスクに応じた `*.instructions.md` を使い分けます。TSDoc コメントのようにプロジェクト全体に適用する標準には、リポジトリ レベルのファイルが適しています。

## 同じプロンプトを再実行して変化を確認する

1. Copilot Chat に戻り、**New Chat** を選択してコンテキストをクリアします。
2. `src/lib/publishers.ts` をもう一度選択し、Copilot が対象ファイルに注目できるようにします。
3. 先ほどと**同じプロンプト**を送ります。

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

4. 提案されたファイルの先頭に、次のようなコメント ブロックがあることを確認します。

   ```typescript
   /**
    * Publisher data-access helpers for the Tailspin Toys Crowd Funding platform.
    * Provides functions to retrieve publisher information from the database.
    */
   ```

5. 提案された関数に、次のような TSDoc コメントがあることを確認します。

   ```typescript
   /**
    * Returns a list of all publishers with their id and name.
    *
    * @param db - The Drizzle database client.
    * @returns A promise that resolves to an array of publisher objects.
    */
   ```

新しいプロジェクト標準に従うよう Copilot を導き、次の演習で利用する実際のコードに適用しました。

## 命令とブランチをコミットしてプッシュする

命令ファイルも、ほかのリポジトリ資産と同じようにソース管理します。命令の更新とヘルパーをコミットしてブランチをプッシュします。

1. <kbd>Control</kbd>+<kbd>`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux) を押して、新しいターミナルを開きます。
2. ターミナルで変更を確認します。

   ```bash
   git status
   ```

3. 命令の更新と、ヘルパーの基盤として Copilot が変更したファイルをステージしてコミットします。

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # If git status shows additional supporting updates (for example tests), add those files too.
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. リポジトリにブランチをプッシュします。

   ```bash
   git push -u origin custom-instructions
   ```

## プル リクエストを作成してマージする

ブランチをプッシュしたら、バックログにあるドキュメント標準の Issue とプル リクエストを関連付けます。GitHub ツールがプロジェクトに接続されているので、Copilot に Issue を探し、PR を作成してマージするよう依頼します。

> [!NOTE]
> この演習では、Copilot が初めて GitHub 上で操作します。プロジェクト テンプレートには GitHub ツールがあらかじめ接続されています。Copilot が初めてツールを使うときに、VS Code で GitHub へのサインインを求められる場合があります。画面の手順に従ってください。後の演習では、この接続に使われる Model Context Protocol (MCP) について確認します。

1. Codespace 内で Copilot Chat を開きます。
2. <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd> (Windows/Linux) を押して Copilot Chat ビューを開き、エージェント選択から **Agent** が選択されていることを確認します。
3. 命令ファイルの更新に関する Issue を探し、現在のブランチから PR を作成するよう Copilot に依頼します。説明には命令の更新と、今後の絞り込み作業に向けた publishers ヘルパーの基盤を含めます。

   ```plaintext
   Find the issue related to updating the instructions file. Create a new PR from the current branch, highlight that the PR closes that issue, and include that we also added the publishers helper foundation for the upcoming filtering work.
   ```

4. Copilot が Issue を探して PR を作成します。
5. GitHub の操作を許可するよう求められたら、コマンドを確認して、適切な場合に **Allow** を選択します。
6. プル リクエスト (PR) が作成されたら、次のプロンプトでマージを依頼し、ブランチを `main` に戻します。

   ```plaintext
   Merge the PR into main. Then return to main locally, and pull the latest code so we are up to date.
   ```

7. GitHub の操作やシェル コマンドを許可するよう求められたら、内容を確認して **Allow** を選択します。

GitHub Copilot の支援でプル リクエストを作成し、マージしました。

## まとめと次のステップ

Copilot が命令ファイルのコンテキストを読み取る方法を確認し、VS Code の Copilot Chat を使って次の作業を行いました。

- 既存の命令でコード生成プロンプトを送り、Copilot の出力を確認しました。
- `.github/copilot-instructions.md` にリポジトリ全体に適用する標準を追加しました。
- 同じプロンプトを再実行し、提案コードが新しい標準に従うことを確認しました。
- 命令の更新とヘルパーの基盤をコミットし、`main` にマージして次の演習で利用できるようにしました。

次は、Copilot がコードベース全体に機能を追加する際に[agent mode で命令を活用します][next-lesson]。

## リソース

- [GitHub Copilot のカスタム命令ファイル][instruction-files]
- [効果的なカスタム命令を作成するためのベスト プラクティス][instructions-best-practices]
- [Copilot のカスタム命令を改善する 5 つのヒント][copilot-instructions-five-tips]
- [GitHub Copilot の個人用カスタム命令][personal-instructions]
- [Awesome Copilot — 命令ファイルなどのリソース集][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
