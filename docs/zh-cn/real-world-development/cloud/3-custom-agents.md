---
title: "练习 3 - 自定义智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## 什么是自定义智能体？

[GitHub Copilot 中的自定义智能体][custom-agents-concept]是针对开发工作流中特定任务或领域定制的人工智能 (AI) 助手。可以在存储库的 `.github/agents` 文件夹中用 Markdown 文件定义智能体，为其提供专门指令、最佳实践、编码模式和领域知识，帮助它更有效地完成特定工作。团队可将专业经验整理为可复用的智能体，例如遵循《Web 内容无障碍指南》 (WCAG) 的无障碍智能体、遵循安全编码实践的安全智能体，或维护一致测试模式的测试智能体。

自定义智能体由项目 `.github/agents` 文件夹或全局 `~/.copilot/agents` 目录中的 Markdown 文件定义。每个文件都包含 YAML 前置元数据 (frontmatter)，至少需要 `name` 和 `description`，后续 Markdown 提示则用于定义智能体行为、专长和指令。

### 自定义智能体与智能体技能的区别

自定义智能体和[智能体技能][agent-skills-concept]都主要通过 Markdown 文件定义，并指导 AI 执行操作。最简单的区分方式是：**自定义智能体是执行工作的角色，技能是它使用的工具**。

自定义智能体拥有自己的上下文窗口，并可在工作中协调技能，甚至协调其他智能体。本实验中的无障碍自定义智能体会根据无障碍指南审查并更新网站；执行任务时，它可以调用拉取请求工作流技能或运行和管理测试的技能。

> [!NOTE]
> 自定义智能体没有唯一正确的写法。与其他 AI 用法一样，应在自己的环境和场景中测试并不断迭代。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

本练习将介绍如何：

- 了解自定义智能体的定义方式。
- 将任务分配给自定义智能体。

## 场景

Tailspin Toys 致力于让所有用户都能使用其众筹平台，不受视觉能力或偏好影响。近期用户反馈指出，当前深色主题的文字与背景对比度不足，难以阅读。设计团队因此要求添加可切换的高对比度模式。

无障碍性至关重要，因此需要尽快实现此功能。你将使用自定义智能体生成相关功能。

## 查看无障碍自定义智能体

项目已包含无障碍自定义智能体。先查看它的内容，了解其如何指导 Copilot。

1. 返回 Codespace，打开 `.github/agents/accessibility.md`。
2. 查看包含 `name` 和 `description` 字段的 YAML frontmatter。

> [!CAUTION]
> 自定义智能体必须包含 `name` 和 `description` frontmatter。

3. 浏览后续部分，查看生成无障碍网站代码时的核心职责、最佳实践、超文本标记语言 (HTML)、层叠样式表 (CSS) 和 JavaScript 示例，以及常见问题。

## 创建并分配议题

任务控制中心是管理环境中所有智能体的中心位置。你可以在那里分配任务、监控任务，也可以重定向并为智能体提供额外指导。现在将创建高对比度模式的任务交给 Copilot。

1. 转到存储库。
2. 选择 **Issues** 选项卡。
3. 选择 **New issue** 打开新议题对话框。
4. 选择 **Blank issue**。
5. 将 **Title** 设置为 `Add high contrast mode to website`。
6. 将 **Description** 设置为：

    ```plaintext
    We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
    ```

7. 选择 **Create** 创建议题。
8. 在右侧选择 **Assign to Copilot**，打开分配对话框。
9. 从自定义智能体列表中选择 **Accessibility agent**。

    ![云智能体分配界面中突出显示自定义智能体和 accessibility 智能体](../../../_images/ex5-select-custom-agent.png)

10. 选择 **Assign**。
11. Copilot 将在后台开始处理任务。

## 总结与后续步骤

本课介绍了 [GitHub Copilot 中的自定义智能体][custom-agents]，即针对特定任务和领域定制的 AI 助手。自定义智能体可将团队的专业知识和标准整理为可复用配置，帮助 Copilot 更有效地完成相关任务。

本课中，你：

- 了解了自定义智能体的定义方式。
- 将任务分配给了自定义智能体。

Copilot 正在实现高对比度模式。接下来，在任务控制中心[监控并引导智能体会话][next-lesson]。

## 资源

- [关于自定义智能体][custom-agents]
- [组织使用自定义智能体前的准备工作][org-custom-agents]
- [企业使用自定义智能体前的准备工作][enterprise-custom-agents]

---

| [← 上一课：GitHub Copilot 云智能体][previous-lesson] | [下一课：监控和管理智能体 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
