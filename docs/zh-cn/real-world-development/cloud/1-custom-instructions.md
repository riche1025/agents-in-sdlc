---
title: "练习 1 - 自定义指令（云智能体）"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：先决条件][previous-lesson] · [下一课：Copilot 云智能体 →][next-lesson]

使用生成式 AI 时，上下文至关重要。如果任务需要以特定方式完成，或 Copilot 需要了解背景信息，应确保它能访问这些信息。[指令文件][instruction-files]可以提供指导，让 Copilot 不仅了解你希望它做什么，也了解你希望它如何完成。

本练习将介绍如何：

- 通过存储库自定义指令和按路径限定的指令文件，向 Copilot 提供项目上下文、编码指南和文档标准。
- 在 `.github/copilot-instructions.md` 中添加新的全局存储库标准。

> [!NOTE]
> 与 VS Code 和 CLI 工作流不同，本练习不会比较提示执行前后的结果。Copilot 云智能体会异步处理 GitHub 议题，因此难以实时并排展示指令的影响。稍后审查云智能体创建的拉取请求时，可以看到指令文件的影响。

## 指令文件

### 场景

Tailspin Toys 有一套开发实践指南和要求，包括：

- 数据层始终需要单元测试。
- 用户界面 (UI) 应采用深色模式并具有现代感。
- 应使用 TypeScript 文档注释 (TSDoc) 记录代码。
- 每个文件开头都应添加注释块，说明文件用途。

使用指令文件可确保 Copilot 根据这些实践执行任务。

### 自定义指令

自定义指令可为 Copilot 提供上下文和偏好，帮助它理解编码风格和要求。你可以为整个存储库或特定文件类型创建指令，以说明编码约定、库和注释风格等。

指令文件有两种：

- `.github/copilot-instructions.md`：每次针对该存储库的请求都会发送此文件。内容应是与大多数 Copilot 对话或 CLI 请求有关的项目级信息，例如技术栈、项目概况、最佳实践和全局指导。
- `.github/instructions/*.instructions.md`：为特定任务或文件类型创建指令，例如 TypeScript、Astro、UI 组件或单元测试。

> [!NOTE]
> 在集成开发环境 (IDE) 中，指令文件仅用于 Copilot Chat 代码生成，不用于代码补全或下一步编辑建议。
>
> Copilot Chat、Copilot CLI（命令行界面）和 Copilot 云智能体在生成代码时都会使用存储库级指令和包含 `applyTo` frontmatter 的 `*.instructions.md` 文件。
>
> Copilot 还[支持其他标准的指令文件][custom-instructions-support]，包括 AGENTS.md 和 CLAUDE.md。

### 管理指令文件的最佳实践

示例项目展示了一种有代表性的做法：

- 将 `copilot-instructions.md` 中的内容限定为项目级指导，例如项目简介、结构和全局编码标准。
- 使用 `*.instructions.md` 为文件类型（单元测试、Astro 组件、数据层）或特定任务提供指导。
- 使用自然语言，确保指导清晰，并提供代码示例说明推荐或不推荐的做法。

指令文件没有唯一的正确写法。你可以通过试验，逐步找到适合项目的方式。

> [!TIP]
> 每个使用 GitHub Copilot 的项目都应包含完善的指令文件。浏览项目文件时，你可能会看到针对 [UI 更新][ui-instructions]和 [Astro][astro-instructions] 等任务的指令。
>
> Copilot 也可以帮助生成指令文件。不同产品界面的操作方式各不相同，例如 VS Code 中的 **Configure Chat → Generate Agent Instructions**，或 Copilot CLI 中的 `/init`。相关课程会在需要时介绍具体操作。
>
> 如需模板或入门示例，可浏览包含指令文件、自定义智能体和其他资源的 [awesome-copilot][awesome-copilot]。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## 查看项目中的自定义指令文件

查看此存储库自带的指令文件：一个核心 `copilot-instructions.md` 文件，以及一组用于不同任务的 `*.instructions.md` 文件。可在编辑器或 GitHub 网页界面中打开它们。

1. 打开 `.github/copilot-instructions.md`。
2. 查看项目简介以及 **Agent notes**、**Code standards**、**Scripts** 和 **Repository Structure** 等部分。查看 **Code standards** 中的 **GitHub Actions Workflows** 子部分。这些指导适用于 Copilot 在此存储库中的交互。
3. 打开 `.github/instructions` 文件夹，浏览其中的 Astro、Drizzle 数据层、测试等指令文件。
4. 打开 `.github/instructions/unit-tests.instructions.md`。查看顶部的 `applyTo` 字段；它设置相对于存储库根目录的 glob，用于确定适用文件。此处会匹配 TypeScript 测试文件，例如符合 `**/*.test.ts` 的文件。
5. 查看此项目的单元测试专用指令。
6. 打开 `.github/instructions/drizzle.instructions.md` 并滚动到底部。查看它指向其他指令文件（例如 `unit-tests.instructions.md`）和项目现有文件的链接。这样可以将较大的指令集拆分成可复用的小文件，并让 Copilot 参考代码示例。相关路径是相对于指令文件所在位置的。

> [!NOTE]
> `copilot-instructions.md` 中的 **Code formatting requirements** 部分介绍了项目编码标准，但尚未要求代码内文档。下一步将添加 TSDoc 文档注释和文件注释头的规则。

## 添加新的存储库标准

接下来要编辑的是唯一文件：添加一项项目级规则，要求使用 TSDoc 文档注释和文件级注释头。稍后的练习中，云智能体处理议题时会读取这项规则。

编辑前，先创建一个分支。云智能体会读取议题目标分支中的指令，但仍应将更改整洁地提交。

1. 在 Codespace 终端中创建并切换到新分支：

   ```bash
   git checkout -b custom-instructions-cloud
   ```

存储库级 `.github/copilot-instructions.md` 用于向 Copilot 提供项目级信息。添加编码标准可以改善代码建议。

2. 重新打开 `.github/copilot-instructions.md`。
3. 找到 **Code formatting requirements** 部分，该部分应位于第 27 行附近。它介绍了项目编码标准，但尚未要求代码内文档，这也是生成的辅助函数没有文档注释的原因。
4. 在现有标准下方添加以下 Markdown 内容，要求 Copilot 添加文件注释头和 TSDoc 文档注释：

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

5. 保存 `copilot-instructions.md`。

> [!TIP]
> 如上一课所示，可在存储库级 `.github/copilot-instructions.md` 中添加全局指令，也可以用 `*.instructions.md` 文件为特定语言、文件类型或任务提供指导。项目级标准（例如文档注释规则）适合放在存储库级文件中。

## 提交、推送并合并指令更新

云智能体会读取议题目标分支上的指令。下一练习将把议题分配给从 `main` 分支创建分支的 Copilot，因此指令更改必须先合并到 `main`。

1. 暂存并提交更改：

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. 推送分支：

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. 在 github.com 上创建从 `custom-instructions-cloud` 合并到 `main` 的拉取请求并完成合并。之后，云智能体处理议题时就会读取这些指令。

> [!TIP]
> 如果希望在本研讨会中直接使用 `main` 分支，可以跳过创建分支，并直接提交到 `main`。此处创建分支是为了模拟真实项目中的工作方式。

## 总结与后续步骤

你了解了 Copilot 如何读取项目指令，并更新了存储库级标准。本课中，你：

- 查看了存储库自定义指令和按路径限定的指令文件。
- 在 `.github/copilot-instructions.md` 中添加了新的全局标准。

接下来，将第一个议题[分配给 Copilot 云智能体][next-lesson]。

## 资源

- [用于自定义 GitHub Copilot 的指令文件][instruction-files]
- [创建自定义指令的最佳实践][instructions-best-practices]
- [编写更好的 Copilot 自定义指令的 5 个技巧][copilot-instructions-five-tips]
- [Awesome Copilot：指令文件和其他资源集合][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
