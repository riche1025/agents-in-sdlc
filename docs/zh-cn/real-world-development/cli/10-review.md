---
title: "第 10 课 - 总结与后续步骤"
description: "回顾 Copilot CLI 工作流、两个拉取请求、可复用的自定义项和更多资源。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

你在 Tailspin Toys 的连续工作流中使用了 GitHub Copilot CLI。本研讨会中，你：

- 准备了 Codespace、安装了 Copilot CLI、探索了项目并找到预置的筛选议题。
- 添加了星级评分，在转发的浏览器中检查结果，并手动合并了第一个拉取请求 (PR)。
- 从筛选议题开始，在 Plan 模式中确定方案、在 Autopilot 模式中实现，并在 Interactive 模式中审查。
- 使用自定义指令引导智能体，自定义现有的 `quality-checks` 技能，并使用它运行单元测试、lint 和类型检查。
- 添加了 Playwright 模型上下文协议 (MCP) 服务器，并在真实浏览器中检查筛选功能。
- 创建并选择质量保证 (QA) 自定义智能体，以评估需求、覆盖范围、技能结果和浏览器证据。
- 审查了完整的筛选更改，并授权 Agent Merge 处理筛选 PR。
- 探索了用于管理上下文、模型、共享和可选云委派的斜杠命令。

## 交付的更改

本研讨会有两个 PR 阶段，每个阶段都基于更新后的 `main` 分支创建独立分支：

1. **星级评分**：在游戏卡片上显示现有的 `starRating` 和明确的未评分状态。
2. **筛选和质量工作流**：实现筛选、更新并应用指令、自定义 `quality-checks` 报告、创建 QA 配置文件，并添加相关测试。

从规划筛选功能到创建其 PR，你一直使用同一对话和分支。为简化研讨会流程，这些工作合并为一个 PR。

## 不同类型的验证

你通过自动化测试、浏览器手动检查和 Copilot 使用 MCP 进行的浏览器探索，以多种方式检查了代码。`quality-checks` 技能运行单元测试、lint 和类型检查，并按你新设定的格式报告结果。QA 智能体还结合需求和测试覆盖范围审查了这些结果。

新增测试应解决实际缺口；QA 检查后发现无需新增测试，也可能是合理结果。合并前应审查代码和证据，并在更改后重新检查受影响的证据。

## 最佳实践

提供给 Copilot 的上下文和工具会影响它的工作方式。在本研讨会中，你更新了指令、自定义技能、创建 QA 配置文件并设置 MCP 服务器。可以在其他对话中复用这些自定义项，并根据团队需求调整。指令设定标准，技能描述可重复任务，自定义智能体定义专业角色，MCP 服务器连接外部工具。应审查实际更改和工具结果，而不只是智能体的总结。

根据任务选择**模式和模型**。使用 **Plan** 先考虑实施方案，使用 **Interactive** 协作完成范围明确的更改，使用 **Autopilot** 处理范围清晰的任务。日常修改可选择速度较快的模型，复杂任务则可选择能力更强的模型。

上下文与基础设施同样重要。清楚地说明希望构建的内容、原因和方式，会显著影响输出。

## 继续探索

你已了解核心工作流。还可以探索以下 CLI 功能：

- `/review`：让代码审查智能体分析更改。
- `/rubber-duck`：讨论问题并获得另一种观点。
- `/fleet`：并行协调彼此独立的子任务。
- `/worktree`：隔离单独任务。
- `/delegate`：将任务交给 Copilot 云智能体。

## 后续步骤

提升工具使用能力的最佳方式就是持续使用。可以将它用于生产代码、个人项目，或一直想做但尚未开始的小应用。与团队分享经验，也向团队成员学习，并继续探索文档。

如果想继续在终端中扩展 Tailspin Toys，可学习可选的 [Foundry Backer Concierge 系列][foundry]。若想比较其他工作环境，可探索 [VS Code 研讨会][vscode]、[GitHub Copilot app 研讨会][app]或 [Copilot 云智能体研讨会][cloud]。

## 资源

- [关于 GitHub Copilot CLI][about-cli]
- [Copilot CLI 命令参考][cli-reference]
- [自定义 Copilot CLI][customize-cli]
- [使用 Copilot CLI 管理拉取请求][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
