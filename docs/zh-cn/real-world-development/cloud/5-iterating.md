---
title: "练习 5：迭代改进 GitHub Copilot 的工作"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 上一课：管理智能体][previous-lesson] |
|:--|

## 审查工作

在本实验中，你使用 GitHub Copilot 完成了多项改善用户体验和添加功能的任务：为代码添加文档、构建供设计团队迭代的相关游戏功能，以及实现高对比度和浅色模式切换等无障碍功能。现在检查代码更改；如有需要，向 Copilot 提供反馈以改进结果。

### 场景

生成式人工智能 (AI) 不会改变软件设计和 DevOps 的基本原则。始终需要审查生成的代码，并遵循常规 DevOps 流程。现在先审查 Copilot 为文档、相关游戏功能和无障碍功能提出的更改，然后再为团队其他成员启用审查。

## GitHub Copilot 云智能体的安全机制

Copilot 云智能体会异步且自主地执行任务。为确保安全，系统采用以下约束：

- Copilot 只能读取存储库，并且只能写入它用于修改代码的分支。
- 云智能体在 GitHub Actions 中运行，并使用单独的临时环境。
- 运行任何 GitHub Actions 工作流前，都需要人工批准。
- 默认情况下，[对外部资源的访问受到限制](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall)，包括对模型上下文协议 (MCP) 服务器的访问。

## 审查生成的文档

先查看 GitHub Copilot 云智能体创建的第一个拉取请求 (PR)，即为代码添加文档的 PR。使用 GitHub.com 上的标准 PR 界面审查。

> [!NOTE]
> 查看 PR 时，可能会看到 GitHub Copilot 被防火墙阻止的警告。这是预期行为，因为默认情况下 Copilot 对外部资源的访问受到限制，包括调用外部 MCP 服务器。如果需要，可以[自定义或禁用 Copilot 云智能体防火墙][agent-firewall]。

1. 返回 github.com 上的存储库。
2. 选择 **Pull Requests** 查看 PR 列表。
3. 打开标题类似 **Add missing documentation** 的 PR。

> [!NOTE]
> 如果 Copilot 仍在处理任务，PR 标题会包含 **[WIP]**。请等待它完成，这可能需要几分钟。

4. PR 准备就绪后，选择 **Files changed** 选项卡并审查更改。

    ![Files changed 选项卡](../../../_images/shared-pr-files-changed.png)

5. 查看新生成的 TypeScript 文档注释 (TSDoc) 和其他文档。具体更改可能有所不同。检查 TSDoc 注释、TypeScript 约定和文件注释头；它们来自练习 2 中查看的自定义指令文件。
6. 审查完成后，返回 **Conversation** 选项卡并向下滚动。
7. 查看是否有工作流等待批准的提示。
8. 如果工作流等待批准，选择 **Approve and run workflows**。

    ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

9. 工作流应在 PR 的检查区域中排队运行。检查单体 Astro 应用的项目检查是否通过；这可能需要几分钟。

## 请求 GitHub Copilot 修改

你可以像在团队成员的 PR 中一样，在 PR 评论或代码行内评论中提及 Copilot。Copilot 会读取评论，并启动新的会话处理要求。由于生成结果具有不确定性，无法规定应使用的确切文本。可以要求 Copilot：

- 在每个代码文件顶部添加简要说明文件用途的注释头。
- 为 TypeScript 和 Astro 文件添加 TSDoc 文档注释。
- 创建 README，介绍 Astro 应用结构。

1. 在评论中提及 **@copilot**，并要求它更新生成的文档。可使用以上建议，也可以提出其他文档改进要求。
2. 选择 **View Session**，观察 Copilot 如何启动新会话进行更新。
3. 选择 **Back to pull request** 返回 PR。

    ![Back to pull request](../../../_images/ex7-back-to-pr.png)

4. Copilot 完成更改后，PR 中应出现新的提交。
5. 选择 **Files changed** 选项卡审查更改。

满意后，可以将 PR 从草稿转换为准备审查状态，并合并到主分支。

![将 PR 转为准备审查状态](../../../_images/ex7-ready-for-review.png)

## 审查相关游戏功能

返回 Copilot 为游戏详情页显示相关游戏的议题创建的 PR。

1. 返回 GitHub.com 上的存储库。
2. 选择 **Pull Requests** 选项卡。
3. 选择标题类似 **Show related games on the game details page** 的 PR。
4. 选择 **Files changed** 选项卡，审查生成的代码。
5. 审查完成后，返回 **Conversation** 选项卡并向下滚动。
6. 查看是否有工作流等待批准的提示。
7. 如果有，选择 **Approve and run workflows**。

    ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

8. 在 PR 检查区域确认工作流排队运行，并确认单体 Astro 应用的项目检查通过。此过程可能需要几分钟。
9. **可选：**在 Codespace 中检出此分支，手动测试相关游戏功能。将 `<branch-name>` 替换为 Copilot 创建的分支名称，例如 **copilot/fix-8**：

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

Copilot 已实现相关游戏功能。与之前一样，可以通过评论继续迭代，例如调整显示的相关游戏数量，或要求添加注释头和 TSDoc 文档注释（该任务是在更新自定义指令之前分配的）。在 **Conversation** 选项卡中添加评论即可让 Copilot 启动新会话。

## 审查无障碍功能

最后，审查由无障碍自定义智能体实现的功能。此 PR 应同时包含练习 3 中分配的高对比度模式，以及练习 4 中在任务控制中心要求的浅色模式。

1. 返回 GitHub.com 上的存储库。
2. 选择 **Pull Requests** 选项卡。
3. 选择标题类似 **Add high contrast mode to website** 的 PR。

> [!NOTE]
> 如果 Copilot 仍在处理任务，PR 标题会包含 **[WIP]**。请等待它完成，这可能需要几分钟。

4. 选择 **Files changed** 选项卡，审查生成的代码。
5. 检查实现，尤其关注：
   - 用于切换模式的界面组件。
   - 用于保存用户偏好的本地存储。
   - 高对比度和浅色模式的层叠样式表 (CSS) 或样式更改。
   - 无障碍属性（无障碍富互联网应用 (ARIA) 标签、键盘导航等）。
   - 管理模式切换的 JavaScript/TypeScript 代码。

6. 审查完成后，返回 **Conversation** 选项卡并向下滚动。
7. 查看是否有工作流等待批准的提示。
8. 如果有，选择 **Approve and run workflows**。

    ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

9. 在 PR 检查区域确认工作流排队运行，并确认单体 Astro 应用的项目检查通过。此过程可能需要几分钟。
10. **可选：**在 Codespace 中检出分支以手动测试无障碍功能。将 `<branch-name>` 替换为 Copilot 创建的分支名称：

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    然后启动应用，在浏览器中测试高对比度和浅色模式切换，并确认页面重新加载后设置仍然有效。

自定义无障碍智能体指导 Copilot 按照无障碍最佳实践实现这些功能。如果发现无障碍问题或改进点，可像处理前面 PR 一样，在评论中提及 **@copilot** 并要求更新。

## 可选练习：继续委派任务

云智能体适合处理待办事项，让你能专注于其他工作。可在存储库中创建更多议题并分配给 Copilot，以培养这种工作习惯。例如：

- 在游戏详情页创建支持者意向表单。
- 为游戏列表页添加分页。
- 为数据访问辅助函数添加输入验证和错误处理。

## 总结

你已完成云智能体工作流。本系列课程中，你：

- **检查了存储库自带的自定义指令文件**，以便之后观察其对云智能体输出的影响。
- **将议题分配给 Copilot 云智能体**，观察它设置环境、规划并异步执行任务。
- **创建并使用自定义智能体**实现无障碍功能，添加高对比度和浅色模式切换。
- **使用 Copilot 智能体页面作为任务控制中心**，监控并引导无障碍会话。
- **审查并迭代云智能体创建的拉取请求**，通过提及 `@copilot` 请求更改并批准工作流。

## 回顾与后续步骤

云智能体工作流已完成。其他工作流可以帮助你继续实践：

- [VS Code 工作流][vscode]：在集成开发环境 (IDE) 中探索 Copilot Chat 智能体模式和 MCP 集成。
- [CLI 工作流][cli]：从终端交付两个经过审查的更改，体验 Plan 和 Autopilot 模式、智能体技能、自定义质量保证 (QA) 智能体、Playwright MCP、Agent Merge，以及可选的 `/delegate` 云智能体桥接。

也可以在自己的存储库中尝试以下后续任务：

- 将重构或测试覆盖率议题分配给云智能体。
- 为其他领域创建自定义智能体。
- 为不同技术栈设置 `copilot-setup-steps.yml`。

## 资源

- [GitHub Copilot][github-copilot]
- [关于 Copilot 智能体][copilot-agents]
- [将 GitHub 议题分配给 Copilot][assign-issue]
- [Copilot 云智能体设置工作流最佳实践][cloud-agent-best-practices]
- [配置 Copilot 云智能体防火墙][agent-firewall]

---

| [← 上一课：管理智能体][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall
[previous-lesson]: ../4-managing-agents/
[vscode]: ../../vscode/
[cli]: ../../cli/
