---
title: "演習 1 - カスタム命令 (Cloud agent)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: 前提条件][previous-lesson] · [次のレッスン: Copilot cloud agent →][next-lesson]

生成 AI を使う際は、コンテキストが重要です。タスクを特定の方法で実行したい場合や、Copilot に知っておいてほしい背景情報がある場合は、そのコンテキストを参照できるようにします。[命令ファイル][instruction-files]を使うと、Copilot に何をしてほしいかだけでなく、どのように作業してほしいかも伝えられます。

この演習では、次のことを行います。

- リポジトリのカスタム命令とパスに応じた命令ファイルを通じて、プロジェクト固有のコンテキスト、コーディング ガイドライン、ドキュメント標準が Copilot に伝わる方法を確認します。
- `.github/copilot-instructions.md` にリポジトリ全体に適用する標準を追加します。

> [!NOTE]
> VS Code や CLI のハーネスとは異なり、この演習では変更前後のプロンプトを比較しません。Copilot cloud agent は GitHub Issue に対して非同期で動作するため、リアルタイムの比較が難しいためです。後続の演習で cloud agent が作成したプル リクエストをレビューする際に、命令ファイルの影響を確認します。

## 命令ファイル

### シナリオ

Tailspin Toys には、開発手法に関するガイドラインがあります。

- データ層には必ずユニット テストを用意します。
- ユーザー インターフェイス (UI) はダーク モードで、現代的な見た目にします。
- コードには TypeScript Documentation (TSDoc) コメントを使ってドキュメントを追加します。
- 各ファイルの先頭に、ファイルの役割を説明するコメント ブロックを追加します。

命令ファイルを使い、Copilot がこれらの開発手法に沿って作業できるようにします。

### カスタム命令

カスタム命令を使うと、コーディング スタイルや要件を Copilot に伝え、より適切な提案やコード スニペットを得られます。リポジトリ全体に適用する命令と、特定のファイル種別やタスクに適用する命令を作成できます。

命令ファイルには、次の 2 種類があります。

- `.github/copilot-instructions.md` は、リポジトリに関するすべてのリクエストで Copilot に送られます。技術スタック、構築しているものの概要、ベスト プラクティスなど、多くのリクエストに関係するプロジェクト全体の情報を記述します。
- `.github/instructions/*.instructions.md` は、TypeScript や Astro などの特定の言語や、UI コンポーネントやユニット テストの作成などのタスクに関するガイドラインを記述します。

> [!NOTE]
> 統合開発環境 (IDE) では、命令ファイルは Copilot Chat のコード生成にのみ使われ、コード補完や次の編集候補には使われません。
>
> Copilot Chat、Copilot CLI、Copilot cloud agent は、コード生成時にリポジトリ レベルの命令と `applyTo` frontmatter を持つ `*.instructions.md` ファイルの両方を使います。
>
> Copilot は AGENTS.md や CLAUDE.md など、別の標準による命令ファイルにも対応しています。詳細は[カスタム命令のサポート状況][custom-instructions-support]を参照してください。

### 命令ファイルを管理するためのベスト プラクティス

命令ファイルの作成に関する詳しい説明はこの演習の範囲外ですが、サンプル プロジェクトには代表的な構成例があります。基本的には、次の点を考慮します。

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

## このプロジェクトのカスタム命令ファイルを確認する

このリポジトリには、`.github/copilot-instructions.md` と、タスク別の `*.instructions.md` ファイルがあります。エディターまたは GitHub Web UI で開いて確認します。

1. `.github/copilot-instructions.md` を開きます。
2. プロジェクトの概要と **Agent notes**、**Code standards**、**Scripts**、**Repository Structure** などのセクションを確認します。**Code standards** の **GitHub Actions Workflows** のガイダンスも確認してください。これらの命令は、Copilot とのあらゆるやり取りに適用されます。
3. `.github/instructions` フォルダーを開き、Astro、Drizzle データ層、テストなどに関する命令を確認します。
4. `.github/instructions/unit-tests.instructions.md` を開き、先頭の `applyTo` フィールドがリポジトリ ルートからの glob を定義していることを確認します。たとえば `**/*.test.ts` に一致する TypeScript テスト ファイルに適用されます。
5. このプロジェクトでユニット テストを作成するための具体的な命令を確認します。
6. `.github/instructions/drizzle.instructions.md` の末尾まで読み、`unit-tests.instructions.md` などの別の命令ファイルや既存ファイルへのリンクを確認します。パスはリポジトリ ルートではなく、命令ファイルからの相対パスです。

> [!NOTE]
> `copilot-instructions.md` の **Code formatting requirements** セクションにはプロジェクトのコーディング標準が記載されていますが、コード内のドキュメント化はまだ必須ではありません。次の手順で TSDoc コメントとファイル ヘッダーの規則を追加します。

## リポジトリ全体に適用する標準を追加する

ここで行う編集は、コード内の TSDoc コメントとファイル コメント ヘッダーを必須にするルールの追加です。後の演習で Issue を割り当てたとき、cloud agent がこの標準を使えるようにします。

編集の前に、命令の変更を個別にコミットできるようブランチを作成します。cloud agent は Issue の対象ブランチから命令を読み込みます。

1. Codespace のターミナルで、新しいブランチを作成して切り替えます。

   ```bash
   git checkout -b custom-instructions-cloud
   ```

2. `.github/copilot-instructions.md` を開き直します。
3. 27 行目あたりの **Code formatting requirements** セクションを探します。既存の標準を確認します。コード内ドキュメントのルールがまだないことにも注目してください。
4. 既存の標準の直後に、次の Markdown を追加します。

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

5. `copilot-instructions.md` を保存します。

> [!TIP]
> 前のセクションで確認したとおり、命令ファイルはリポジトリ全体に適用する `.github/copilot-instructions.md` と、言語、ファイル種別、タスクごとの `*.instructions.md` に分けられます。TSDoc コメントのようなプロジェクト全体の標準には、リポジトリ レベルのファイルが適しています。

## 命令の変更をコミット、プッシュ、マージする

cloud agent は、Issue の対象ブランチにある命令ファイルを読み込みます。次の演習では Issue を `main` から Copilot に割り当てるため、cloud agent が新しい命令を使えるように、変更を `main` にマージします。

1. 変更をステージしてコミットします。

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. ブランチをプッシュします。

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. github.com で `custom-instructions-cloud` から `main` へのプル リクエストを作成してマージします。次の演習で Issue を割り当てると、cloud agent は更新された命令を読み込みます。

> [!TIP]
> このワークショップでは `main` に直接作業してもかまいません。その場合はブランチの作成を省略して、`main` に直接コミットできます。ここでは実際のプロジェクトの作業方法に近づけるためにブランチを使っています。

## まとめと次のステップ

このプロジェクトの命令ファイルから Copilot がコンテキストを読み取る方法を確認し、`.github/copilot-instructions.md` にリポジトリ全体の標準を追加しました。残りのハーネスで cloud agent が作成するプル リクエストをレビューする際に、この標準の効果を確認できます。

次は、[最初の Issue を Copilot cloud agent に割り当てます][next-lesson]。

## リソース

- [GitHub Copilot のカスタム命令ファイル][instruction-files]
- [効果的なカスタム命令を作成するためのベスト プラクティス][instructions-best-practices]
- [Copilot のカスタム命令を改善する 5 つのヒント][copilot-instructions-five-tips]
- [Awesome Copilot — 命令ファイルなどのリソース集][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
