---
title: "レッスン 4 - カスタム命令で Copilot を導く"
description: "リポジトリの命令を確認し、ドキュメント標準を追加して、絞り込み機能のコードに適用します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

生成 AI を使う際は、コンテキストが重要です。タスクを特定の方法で実行したい場合、その指針を Copilot が参照できるようにします。[命令ファイル][instruction-files]には、求めるコードだけでなく、その構成方法も記述できます。絞り込み機能を実装したので、Copilot が参照した命令を確認し、ドキュメント標準を追加して、コードに適用します。

このレッスンでは、次のことを行います。

- リポジトリの命令とパスに応じた命令ファイルがエージェントに適用される方法を確認します。
- コーディング標準に従うよう、命令ファイルを更新します。
- 命令ファイルがコードに与える影響を確認します。

## シナリオ

Tailspin Toys には、開発手法に関するガイドラインがあります。

- コメントには、コードの言い換えではなく、意図や自明でない判断を記述します。
- `db/` と `src/lib/` のエクスポート関数には、目的、パラメーター、戻り値を説明する TypeScript Documentation (TSDoc)/JavaScript Documentation (JSDoc) を記述します。`db` 引数を注入できる関数では、その引数についても記述します。
- 再利用可能な Astro コンポーネントには `Props` の契約を記述し、関連コードが変わった場合はコメントを最新の状態に保ちます。
- 既存のフォーマットと lint のガイダンスを維持します。

命令ファイルを使い、Copilot がこれらの開発手法に沿って作業できるようにします。

## 命令ファイル

カスタム命令を使うと、コーディング スタイルや要件を Copilot に伝え、より適切な提案やコード スニペットを得られます。リポジトリ全体に適用する命令と、特定のファイル種別に適用する命令を作成できます。

命令ファイルには、次の 2 種類があります。

- `.github/copilot-instructions.md` は、リポジトリに関するすべてのリクエストで Copilot に送られる単一の命令ファイルです。多くのリクエストに関係するプロジェクト全体の情報を記述します。
- `.github/instructions/*.instructions.md` は、特定の言語、ファイル種別、タスクに関するガイドラインを記述します。

> [!NOTE]
> その他の命令形式やサポート状況は、環境によって異なります。形式に依存する前に、[カスタム命令のサポート状況][custom-instructions-support]を確認してください。

## このプロジェクトのカスタム命令ファイルを確認する

スターター プロジェクトには、リポジトリ全体の命令とタスク別の命令ファイルがすでに含まれています。変更を加える前に、既存の内容を確認します。

1. Codespace に戻ります。
2. Codespaces エディターで `.github/copilot-instructions.md` を開きます。ターミナルではなく、エディターで開いてください。
3. プロジェクトの簡単な説明とコーディング ガイダンスを確認します。この命令は、このリポジトリでの Copilot とのすべてのやり取りに適用されます。
4. `.github/instructions` フォルダーを開き、ファイルを確認します。Astro、Drizzle データ層、テストなどに関する命令があります。
5. `.github/instructions/unit-tests.instructions.md` を開きます。先頭の `applyTo` フィールドが、適用対象のファイルを決める glob であることを確認します。
6. `.github/instructions/drizzle.instructions.md` を開き、他の命令ファイルや既存のプロジェクト ファイルへのリンクを確認します。大きな命令セットを再利用可能な小さなファイルに分け、例を参照させることができます。

## チームのガイダンスに合わせて命令ファイルを更新する

現在の命令ファイルには改善の余地があります。新たに生成する TypeScript に TSDoc コメントを追加するよう、`.github/copilot-instructions.md` を更新します。

1. `.github/copilot-instructions.md` で、35 行目あたりにある **Code formatting guidance** セクションを探します。
2. セクションの最後に、次の箇条書きを追加します。

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

ファイルは自動的に保存されます。

## 更新したガイダンスを適用する

Copilot CLI は会話の開始時にリポジトリの命令を読み込みます。命令を保存した後、絞り込みの会話を終了して再開すると、機能のコンテキストを保ったまま新しいガイダンスを読み込めます。

1. 絞り込みの会話が開いている場合は、`/exit` を入力して閉じます。Copilot CLI は会話を自動的に保存します。
2. リポジトリのルートで `game-filters-cli` ブランチに切り替わっていることを確認し、保存済みの会話を再開します。

   ```bash
   copilot --resume
   ```

   プロンプトが表示された場合は絞り込みの会話を選択し、`game-filters-cli` ブランチがチェックアウトされていることを確認します。
3. 次のプロンプトで更新したガイダンスを適用します。

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

4. `/diff` を入力して、変更された TypeScript ファイルを確認します。新しい TSDoc コメントが追加され、コードを正確に説明していることを確認します。

## まとめと次のステップ

Copilot CLI が命令ファイルのコンテキストを使う方法を確認し、新しい標準を機能に適用しました。このレッスンでは、次のことを行いました。

- リポジトリの命令とパスに応じた命令ファイルがエージェントに適用される方法を確認しました。
- 命令ファイルを更新して、コーディング標準が守られるようにしました。
- 命令ファイルがコードに与える影響を確認しました。

次は、再利用可能な `quality-checks` スキルを[カスタマイズして実行し][next-lesson]、lint とテストを一貫して実行します。

## リソース

- [Copilot CLI のカスタム命令を追加する][instruction-files]
- [カスタム命令のサポート状況][custom-instructions-support]
- [効果的なカスタム命令を作成するためのベスト プラクティス][instructions-best-practices]
- [Awesome Copilot — 命令ファイルなどのリソース集][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
