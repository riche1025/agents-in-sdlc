---
title: "练习 2 - GitHub Copilot 云智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 上一课：自定义指令][previous-lesson] |
|:--|

许多组织都面临技术债务，例如尚未解决的安全问题、需要更新的旧代码，或因缺少时间而长期搁置的功能请求。GitHub Copilot 云智能体可以自主更新代码和添加功能。完成后，它会创建草稿拉取请求 (PR)，供开发者审查。这样可以把繁琐任务交给智能体，加快开发流程，让开发者专注于更重要的工作。

本练习将介绍如何：

- 自定义代码生成环境。
- 确保操作安全执行。
- 编写范围清晰的议题。
- 将议题分配给 Copilot。

## 场景

Tailspin Toys 有一些待处理的技术债务。最初开发网站的外包团队没有为代码编写文档。首先，团队希望为应用中所有导出的函数添加 TypeScript 文档注释 (TSDoc)。

此外，设计团队希望改进游戏发现功能。他们想在每款游戏的详情页显示相关游戏（即同一类别中的其他游戏），方便用户继续浏览。当前不要求实现完善功能，只需要可用于用户体验验收测试的版本。虽然这项工作目前受阻，但其他议题优先级更高。

这些任务可能会被不断推迟，很适合交给 Copilot 云智能体异步处理。开发者可继续处理其他工作，之后再回来审查智能体的成果。

## 了解 GitHub Copilot 云智能体

[GitHub Copilot 云智能体](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent)可以像开发者一样在后台执行任务。可以通过多种方式启动任务，例如[将 GitHub 议题分配给 Copilot](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions)。分配后，Copilot 会创建草稿拉取请求以跟踪进度、设置环境并开始处理任务。你可以在会话进行中或完成后查看它的工作。方案准备好审查时，Copilot 会在拉取请求中通知你。

## 明确任务范围的重要性

GitHub Copilot 不会替代思考。即使看似简单的操作，也可能包含复杂细节，因此应谨慎[设定云智能体任务范围][cloud-agent-best-practices]。将它视作 AI 结对编程伙伴：分阶段工作、学习、试验并不断调整。生成式 AI 不会改变软件开发的基本原则。

## 查看此存储库中的自定义指令

之前的练习介绍了自定义指令及其作用。如果已完成自定义指令练习，就已看到 `.github/copilot-instructions.md` 的效果；如果还没有，现在可以快速查看。分配任务给 Copilot 云智能体前，先只读查看存储库中的指令文件，稍后便于观察其影响。

1. 在 GitHub 网页界面或已运行的 Codespace 中打开 `.github/copilot-instructions.md`，查看 **Code standards** 部分，尤其是 TypeScript 约定和 TSDoc 文档注释要求。
2. 打开 `.github/instructions/unit-tests.instructions.md`，查看 `applyTo` frontmatter。它将指令限定在 `**/*.test.ts` 文件。

下一节将 `Code lacks documentation` 议题分配给云智能体时，留意拉取请求中的 TSDoc 注释、TypeScript 约定和文件注释头。这些内容来自上述指令文件。后续练习会再次检查它们。

## 设置云智能体开发环境

创建代码通常需要特定环境和安装脚本，以确保环境准备就绪。将任务分配给 Copilot 时也一样，因为它会以类似软件工程师的方式工作。

云智能体使用 [GitHub Actions][github-actions] 执行工作。可以在 `.github/workflows/copilot-setup-steps.yml` 中配置[专用设置工作流][setup-workflow]，让它在云智能体开始工作前运行，以安装所需工具和依赖项。实验已预先配置此工作流，方便你顺利完成练习并了解相关功能。它会为单体 Astro 应用安装 Node.js、项目依赖项、端到端测试浏览器以及已迁移和填充数据的 SQLite 数据库：

```yaml
name: "Copilot Setup Steps"

# 可从存储库的 "Actions" 选项卡手动测试设置步骤
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # 仅为这些步骤授予所需的最低权限。Copilot 会使用自己的令牌执行操作。
    permissions:
      # 如果要在设置步骤中克隆存储库（例如安装依赖项），需要 `contents: read` 权限。如果未在设置步骤中克隆存储库，Copilot 会在步骤完成后自动克隆。
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # 前端/应用设置：Node.js（整个应用现在使用 Astro 和 Drizzle/libSQL）
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

      # 迁移并填充本地 SQLite 数据库，为构建和测试准备数据。
      - name: Set up the database
        run: npm run db:setup
```

该文件与其他 GitHub 工作流相似，但有几个要点：

- 它包含一个名为 `copilot-setup-steps` 的作业。Copilot 开始处理拉取请求前，GitHub Actions 会运行此作业。
- `workflow_dispatch` 触发器可让你从存储库的 **Actions** 选项卡手动运行工作流。这有助于测试工作流，而不必等待 Copilot 启动它。

## 添加文档

项目经常存在过时或缺失的文档，导致工作效率降低，并增加维护代码库或引入新开发者的难度。Copilot 擅长创建文档，因此很适合将这类技术债务议题交给云智能体。它会在后台生成文档，稍后的练习将审查其成果。

1. 在新浏览器选项卡中转到 github.com 上的存储库。
2. 选择 **Issues** 选项卡。
3. 选择 **New issue** 打开新议题对话框。
4. 选择 **Blank issue**。
5. 在 **Title** 中输入 `Code lacks documentation`。
6. 在 **Description** 中输入：

    ```plaintext
    Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
    ```

7. 选择 **Create** 创建议题。
8. 在右侧选择 **Assign to Copilot**，打开分配对话框。

    ![将议题分配给 Copilot](../../../_images/shared-assign-copilot.png)

9. 选择 **Assign**。

    ![Copilot 议题分配详情](../../../_images/ex4-assign-copilot-details.png)

10. 选择 **Pull Requests** 选项卡。
11. 打开新生成的拉取请求 (PR)，标题可能类似于 `[WIP]: Code lacks documentation`。如果列表中尚未显示新 PR，请稍等片刻并刷新浏览器。
12. 几分钟后，Copilot 应会创建待办事项列表。

> [!NOTE]
> Copilot 创建待办事项列表可能需要几分钟。它正在创建环境（运行前面介绍的工作流）、分析项目并确定处理任务的方案。

13. 查看 Copilot 计划完成的任务。
14. 向下滚动 PR 时间线，确认 Copilot 已开始处理议题。
15. 选择 **View session** 按钮。

    ![Copilot 会话视图](../../../_images/ex4-view-session.png)

> [!CAUTION]
> 可能需要刷新窗口才能看到更新后的状态指示器。

16. 浏览实时会话，观察 Copilot 如何探索代码、了解当前状态、暂停思考并决定方案，然后创建代码。

整个过程可能需要几分钟。云智能体的主要优势之一是异步执行任务，让你可以处理其他工作。接下来利用这一点，再分配一项任务，然后转而开发应用功能。

## 为游戏详情页添加相关游戏

云智能体的一大优势是可以分配并行任务，让你在它处理一项工作的同时处理其他事项。现在把为设计团队添加相关游戏区域的任务交给云智能体。

1. 返回 github.com 上的存储库。
2. 选择 **Issues** 选项卡。
3. 选择 **New issue** 打开新议题对话框。
4. 选择 **Blank issue** 使用空白模板。
5. 将 **Title** 设置为 `Show related games on the game details page`。
6. 在 **Description** 中输入：

    ```markdown
    We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
    ```

7. 选择 **Create** 创建议题。
8. 在右侧选择 **Assign to Copilot**，打开分配对话框。

    ![将议题分配给 Copilot](../../../_images/shared-assign-copilot.png)

9. 选择 **Assign**。

稍后，议题的第一条评论旁会出现 👀，表示 Copilot 已开始处理。

![Copilot 使用眼睛表情符号表示正在处理议题](../../../_images/ex4-issue-eyes-emoji.png)

Copilot 正在处理第二项请求。它的工作方式类似软件工程师，无需持续监控，待任务完成后再进行审查即可。现在可以转而创建和使用自定义智能体。

## 总结与后续步骤

本课介绍了 [GitHub Copilot 云智能体][copilot-agents]。可以将议题分配给云智能体，让它异步工作，以处理技术债务、创建功能或协助迁移代码框架。

本课中，你：

- 自定义了代码生成环境。
- 了解了如何安全执行操作。
- 了解了清晰界定议题范围的重要性。
- 将议题分配给 Copilot。

云智能体正在后台工作，接下来创建并使用自定义智能体。Copilot 云智能体也支持模型上下文协议 (MCP) 服务器，并可以使用之前课程中介绍的自定义指令。

## 资源

- [关于 Copilot 云智能体][copilot-agents]
- [将 GitHub 议题分配给 Copilot][assign-issue]
- [Copilot 云智能体设置工作流最佳实践][cloud-agent-best-practices]

| [下一课：自定义智能体 →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
