---
title: "练习 4 - 监控和管理智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

前两项练习中，你让 Copilot 云智能体分别处理了三项任务，以改善用户体验并添加功能。云智能体虽然能够异步自主工作，但监控任务仍然很重要。

你可以使用多种工具管理分配给云智能体的任务，包括 GitHub.com 上的[智能体页面][agents-page]。在这个任务控制中心，可以查看所有带有未关闭拉取请求 (PR) 的智能体任务、检查智能体执行的操作，还可以引导正在进行的会话。

本课将介绍如何：

- 使用智能体页面监控云智能体任务。
- 引导正在进行的会话，要求添加其他功能。

## 场景

团队要求智能体创建高对比度模式后，意识到也可以顺便添加浅色模式。由于智能体已经在更新网站样式并添加切换功能，因此你希望引导它同时实现浅色模式和高对比度模式。

## 查看 Copilot 云智能体任务

查看当前分配给 Copilot 云智能体的任务状态。

1. 转到 [Copilot 智能体页面](https://github.com/copilot/agents)。
2. 查看主区域和左侧区域中的任务列表。列表应包含你分配给 Copilot 的任务，例如：
   - 更新代码文档。
   - 创建用于修改游戏的应用程序编程接口 (API)。
   - 为网站添加高对比度模式。
3. 选择一项正在运行的任务，查看 Copilot 已执行的工作，例如检出存储库代码、创建工作环境、设置模型上下文协议 (MCP) 服务器以及完成任务的其他步骤。

> [!NOTE]
> 具体显示的步骤因任务状态和 Copilot 采用的方法而异。

4. 查看右侧显示的 PR 面板，以监控 PR 和更改文件。

## 引导云智能体

查看正在进行的任务后，要求 Copilot 在实现高对比度模式的同时添加浅色模式。

1. 选择有关添加高对比度模式的会话。具体标题因 Copilot 使用的名称和任务状态而异。

    ![任务控制中心中的无障碍会话](../../../_images/ex6-accessibility-session.png)

2. 等待几分钟，直到会话显示已完成设置并开始工作。此时应能看到类似的消息。
3. 在 **Steer active session while Copilot is working** 对话框中，输入以下提示：

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![智能体页面中突出显示用于引导活动会话的对话框](../../../_images/ex6-steer-cloud-agent-task.png)

4. 按 <kbd>Enter</kbd> 发送提示。
5. 注意 Copilot 会确认收到提示，并将其纳入任务流程。

## 等待 Copilot 完成工作

Copilot 会继续处理更新后的任务。在完成发送提示时正在执行的步骤后，它会把新要求纳入工作流程。

这可能需要几分钟。等待时，可以回顾目前学到的内容。

## 总结与后续步骤

本课介绍了 Copilot 智能体页面，这是监控和引导 GitHub Copilot 云智能体任务的中心。你可以跟踪所有进行中和已完成的任务、审查智能体正在执行的工作，还可以调整正在进行任务的范围或提供额外指导。

本课中，你：

- 使用任务控制中心和智能体页面监控了云智能体任务。
- 引导了正在进行的会话，要求添加其他功能。

Copilot 正在完成无障碍功能。接下来，[迭代 Copilot 创建的拉取请求][next-lesson]。

## 资源

- [Copilot 智能体页面][agents-page]
- [关于自定义智能体][custom-agents]

---

| [← 上一课：自定义智能体][previous-lesson] | [下一课：迭代 Copilot 的工作 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
