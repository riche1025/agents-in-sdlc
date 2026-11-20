---
title: "练习 2 - 使用 Copilot 智能体模式添加功能"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

即使是简单的应用更新，通常也需要修改多个文件并运行测试。开发者需要找到所有相关文件、进行修改、运行测试、调试、发现遗漏的文件并继续修改。Copilot 智能体模式可以更自主地处理这些工作：探索项目结构、执行必要更新、运行测试，并自动修复发现的问题。现在使用智能体模式为网站添加功能。

> [!NOTE]
> 智能体模式和云智能体名称相似，但适用于不同的工作方式。智能体模式在集成开发环境 (IDE) 中执行任务，可快速反馈并与开发者交互。云智能体则像团队成员一样异步工作，通过议题和拉取请求与你协作。

本练习将介绍如何：

- 使用 Copilot 智能体模式探索项目、查找相关文件并协调更改。
- 使用 GitHub Copilot 智能体模式跨界面和数据层实现功能。
- 在合并到代码库前审查 Copilot 智能体模式生成的更改和测试。

## 场景

游戏列表不断增长，你希望用户可以按类别和发行方筛选。上一练习已添加发行方辅助函数，现在使用 Copilot 智能体模式完成数据层、界面和测试中的其余工作。

## 运行 Tailspin Toys 网站

更改前，先浏览 Tailspin Toys 网站，了解现有功能。

该网站是一个以开发者为主题的桌游众筹平台，可列出游戏并显示详情。它是一个单体 Astro 应用，在构建时将页面渲染为静态超文本标记语言 (HTML)。页面通过 frontmatter 使用 Drizzle 对象关系映射 (ORM) 直接查询本地 SQLite 数据库；没有独立后端应用程序编程接口 (API) 或客户端用户界面 (UI) 框架。可复用的数据访问辅助函数位于 `src/lib/`，交互功能通过少量使用文档对象模型 (DOM) API 的 Astro `<script>` 实现。

### 启动网站

项目提供了 `npm run dev` 任务，用于启动单体 Astro 开发服务器。

1. 返回 Codespace。上一练习结束后，你应已切回 `main`。
2. 按 <kbd>Control</kbd>+<kbd>\`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>\`</kbd>（Windows/Linux），在 Codespace 中打开新终端。
3. 创建并切换到筛选功能分支：

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. 运行以下命令启动网站：

   ```bash
   npm run dev
   ```

   Astro 开发服务器就绪后，应会显示类似以下内容的横幅：

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> 如果弹出对话框，询问是否打开 `http://localhost:4321` 的浏览器窗口，请选择 **x** 将其关闭。

5. 按住 <kbd>Command</kbd>（Mac）或 <kbd>Ctrl</kbd>（Windows/Linux），然后在终端中选择 Astro 服务器地址 `http://localhost:4321`，打开网站。

> [!NOTE]
> 在 Codespace 中选择终端的 localhost 链接时，会自动重定向到 `https://<your-codespace-name>-4321.app.github.dev/`。这是指向 Codespace 的私有隧道，Web 服务器通过它对外提供服务。

### 浏览网站

网站运行后，可以查看现有功能：

- **主页**：显示桌游列表，包括标题、图片和简介。
- **游戏详情页**：选择游戏后，会打开详情页，其中包含标题、简介、发行方和类别等信息。

## 使用 Copilot 查看待办事项

> [!TIP]
> **打开 Copilot Chat**
>
> 开始以下练习前，返回 Codespace，打开 Copilot Chat 面板并选择 **New Chat**，开始干净的对话。模式和模型选择因练习而异；每个相关步骤都会说明。

网站初始版本可以正常运行，但还需要添加更多功能。项目模板会自动创建待办议题，让 GitHub Copilot 显示这些项目。

1. 在 Chat 视图的智能体下拉菜单中选择 **Agent**。该智能体会自主规划并跨文件实现更改、运行终端命令并调用工具。

   ![Chat 视图中的智能体选择器](../../../_images/shared-chat-mode-selector.png)

2. 从可用模型列表中选择 **Claude Sonnet 4.5**。

> [!CAUTION]
> 本研讨会作者并未偏好某个模型。编写研讨会时使用的是 Claude Sonnet 4.5，因此示例使用该模型，以便代码建议相对一致。不过，大型语言模型 (LLM) 的输出具有概率性，收到的建议可能与示例不同，这是正常现象。

> [!NOTE]
> Copilot 可能会使用不同的模型上下文协议 (MCP) 命令，但仍应能完成任务。

3. 发送以下提示，询问 Copilot 待办事项：

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. 选择 **Continue** 运行列出所有议题的命令。
5. 查看生成的议题列表。

Copilot 还会根据它认为对用户最有用的内容为议题排序。

## 查看指令文件

让智能体生成代码前，先查看用于向 Copilot 提供上下文的指令文件。本练习将使用 [UI 指令文件](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md)，其中介绍了为网站添加功能的方式。

1. 在 Codespace 中打开 `.github/instructions/ui.instructions.md`。
2. 查看整体指导，包括：
   - 架构概述。
   - 组件设计、可测试性和无障碍原则。
   - 指向 Astro、Tailwind CSS 和 Drizzle 等特定文件类型指令的链接。

> [!TIP]
> 指令文件可以引用其他指令文件和项目文件。路径相对于指令文件所在位置，因此可以复用内容、拆分复杂指令，并提供示例和模板。

## 实现筛选功能

完成筛选至少需要对应用程序进行三项更新：

- 在数据层 (`src/lib/`) 添加或完善筛选逻辑。
- 添加或更新筛选行为测试。
- 更新游戏列表页，添加筛选界面。

合并前还需要运行并通过测试。Copilot 智能体模式可以完成这些工作。

1. 继续当前 Copilot 对话，或选择 **New Chat** 开始新对话。
2. 选择 **Add Context**、**Instructions** 和 **ui** 指令文件。

   ![选择 UI 指令文件的示例](../../../_images/ex3-select-instructions-file.png)

3. 确认 Chat 视图的智能体下拉菜单中仍选择 **Agent**。

   ![Chat 视图中的智能体选择器](../../../_images/shared-chat-mode-selector.png)

4. 确认仍选择模型 **Claude Sonnet 4.5**。
5. 使用待办事项中相关议题的要求，提示 Copilot 实现功能：

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. 观察 Copilot 探索项目并查找相关文件，包括数据层辅助函数、界面和测试。之后它会修改文件并运行测试。

   ![Copilot 正在探索项目文件](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot 会探索项目、修改文件并运行测试，这可能需要几分钟。过程中编辑器可能会显示 **Keep** 和 **Undo** 控件。Copilot 完成后，所有更改都会提供 **Keep** 或 **Undo** 控件，无需在工作进行中选择。

7. Copilot 提示时，选择 **Continue** 运行测试。

   ![Copilot Chat 提示用户确认运行测试](../../../_images/ex3-agent-mode-run-tests.png)

8. Copilot 处理代码和测试时可能会暂停，测试也可能暂时失败。它会继续迭代，直到完成任务且不再发现错误。
9. 检查生成的代码是否存在问题。

> [!CAUTION]
> 始终需要审查 Copilot 或其他人工智能 (AI) 工具生成的代码。

10. 返回正在运行网站的浏览器，体验新功能。
11. 确认功能正常并审查代码后，在 Copilot Chat 窗口中选择 **Keep**。

## 总结与后续步骤

本练习介绍了如何使用 GitHub Copilot 智能体模式为 Tailspin Toys 网站添加功能。本课中，你：

- 使用 Copilot 智能体模式探索项目、查找相关文件并协调更改。
- 使用 Copilot 智能体模式跨界面和数据层实现了新功能。
- 在合并到代码库前审查 Copilot 智能体模式生成的更改和测试。

接下来，使用 [Playwright MCP 服务器测试功能][next-lesson]，并为其创建拉取请求。

### 额外探索：实现分页

随着游戏列表不断增长，需要添加分页。使用本练习中学到的技能，提示 Copilot 为网站添加分页。编写提示时可考虑：

- 遵循现有最佳实践，包括使用已有指令文件。
- 确定分页方式，例如是否允许用户选择每页条目数，还是使用固定数量。
- 提供 Copilot 所需指导，确保实现符合预期。
- 根据需要与 GitHub Copilot 迭代，通过后续提示提出更改并补充上下文。这是正常的协作流程。

## 资源

- [Copilot 的 ask、edit 和 agent 模式：用途和适用时机][choose-mode]
- [VS Code 中的智能体模式][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
