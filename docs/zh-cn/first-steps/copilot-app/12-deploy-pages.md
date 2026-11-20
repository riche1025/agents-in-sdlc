---
title: "第 12 课 - 使用 GitHub Pages 部署网站"
description: "使用 GitHub Copilot app 配置 Pages 工作流、审查拉取请求，并验证 Space Quiz 是否已上线。"
authors:
  - jamesmontemagno
lastUpdated: 2026-10-12
---

为 Space Quiz 部署一个公开网站。Copilot 可以准备工作流并指导部署，但仍需由你审查更改并确认网站已上线。

本课将介绍如何：

- 让 Copilot 配置 GitHub Pages 部署。
- 在合并前审查工作流和拉取请求。
- 跟进部署并验证已发布的网站。

## 场景

Space Quiz 已在 GitHub 存储库中，但用户还需要一个简单的试用入口。使用 GitHub Pages 发布这个单文件网站，无需添加服务器或运行时依赖项，即可通过公开 URL 访问。

## 让 Copilot 准备部署

先让 Copilot 创建部署工作流和拉取请求。创建拉取请求可能会提交并推送代码，因此在发送提示前请检查批准设置和目标存储库。

1. 在 `space-quiz` 的 Copilot app 会话中，发送以下提示：

   ```plaintext
   Prepare a GitHub Pages deployment for this repository. Create a GitHub Actions workflow that builds the website if needed and deploys it to GitHub Pages after changes reach the default branch. Add a README describing the app and how to run it locally if one does not already exist. Create a pull request with these changes and report its link and any required Pages settings or permissions. Do not merge, enable auto-merge, change Pages settings, or deploy. Stop and wait for my review.
   ```

   使用 **Approve all** 时，不要期待每项操作都会再次要求确认。

## 审查工作流和拉取请求

在授权合并前，确认工作流只会按预期部署，并且所有更改都经过审查。

1. 确认只有在存储库尚无 README 时才添加 README。
2. 审查拉取请求中的更改，包括工作流的构建和部署步骤、触发条件及权限。
3. 确认工作流从默认分支部署，而不是从尚未合并的拉取请求部署。
4. 如需修正，请提出要求并审查更新后的差异。授权合并前，等待必需的拉取请求检查通过。

## 授权合并和部署

以下提示会授权智能体合并已审查的拉取请求、更改存储库 Pages 设置并发布网站。只有在完成审查并确认存储库和拉取请求无误后，才发送此提示。根据批准设置，这些操作可能无需再次确认。

1. 将 `<PR_NUMBER>` 替换为已审查的拉取请求编号，然后单独发送以下提示：

   ```plaintext
   I have reviewed pull request <PR_NUMBER> in this repository and authorize its merge and deployment. Enable GitHub Pages using GitHub Actions, merge that pull request only after required checks pass, and monitor the deployment until it succeeds. Report the final URL of the live website. If you lack permission to enable Pages or merge, tell me exactly what I need to approve or do; do not report success until the site is live.
   ```

![三阶段示意图：已合并的 space-quiz 拉取请求；GitHub Actions 中成功运行的 Deploy website 工作流，包含 Build website、Upload artifact 和 Deploy to Pages 步骤；以及位于 yourname.github.io/space-quiz/ 的在线 Space Quiz。](../../../_images/first-steps-app-pages-deploy.svg)

## 验证部署

部署完成后，确认操作运行成功且公开网站可以加载。

1. 跟进 GitHub Actions 部署运行，直到成功。
2. 打开报告中的 URL，确认 Space Quiz 已加载。

如果智能体无法启用 Pages 或合并拉取请求，请按其提供的具体说明操作。只有部署成功且网站可以加载，任务才算完成。

## 总结与后续步骤

Space Quiz 已作为网站上线，并且你亲自验证了部署，而不是只依赖智能体的报告。本课中，你：

- 让 Copilot 准备了 GitHub Pages 部署。
- 在合并前审查了工作流和拉取请求。
- 跟进部署并验证了已发布的网站。

接下来，继续[回顾并了解后续步骤][next-lesson]。

[next-lesson]: ../13-review/
