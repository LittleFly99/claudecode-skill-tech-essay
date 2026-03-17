# Claude Skill 从入门到精通：5 步打造你的专属 AI 助手

## 前言

在日常开发中，你是否遇到过这样的场景：每次写完代码都要手动执行一套固定的检查流程？团队协作时，每个人的代码风格和提交规范难以统一？某些重复性的开发任务，明明流程固定却每次都要从头开始？

Claude Skill 就是为了解决这些问题而生的。它允许你将固定的流程、规范和最佳实践封装成可复用的"技能"，让 AI 按照你定义的方式工作。

读完本文，你将掌握：
- Claude Skill 的核心概念和工作原理
- Skill 的完整结构和配置规范
- 如何从零开发一个实用的自定义 Skill
- Skill 开发的最佳实践和注意事项

阅读本文需要：
- 基础的 Claude Code 使用经验
- 了解 Markdown 语法
- 熟悉命令行操作

---

## 什么是 Claude Skill？

### 一句话定义

**Claude Skill 是一套可复用的提示词模板，它定义了 AI 在特定场景下的行为模式和执行流程。**

### 为什么需要 Skill？

在没有 Skill 之前，我们使用 Claude Code 的方式通常是这样的：

```
用户：帮我分析这段代码的性能问题
Claude：（执行分析）

用户：帮我生成 commit 信息
Claude：（生成 commit）
```

每次都需要重新描述需求，AI 的输出风格和质量也难以保持一致。

**Skill 解决了什么问题？**

| 问题 | Skill 如何解决 |
|------|---------------|
| 重复描述需求 | 封装成固定流程，一键触发 |
| 输出风格不一致 | 预定义模板和规范 |
| 团队协作难标准化 | 共享 Skill 文件，统一行为 |
| 最佳实践难落地 | 将最佳实践固化在 Skill 中 |

### Skill 的触发方式

Skill 可以通过两种方式触发：

1. **斜杠命令**：输入 `/skill-name` 直接调用
2. **自动触发**：根据 TRIGGER 条件自动识别场景

---

## Skill 的核心结构

一个完整的 Skill 由以下部分组成：

### 目录结构

```
.claude/skills/
└── your-skill/
    ├── SKILL.md          # 主配置文件（必需）
    ├── templates/        # 模板文件（可选）
    │   └── example.md
    └── references/       # 参考文档（可选）
        └── guide.md
```

### SKILL.md 核心配置

```markdown
# Skill 名称

简要描述这个 Skill 的作用。

## 触发条件

TRIGGER when: [触发条件描述]
DO NOT TRIGGER when: [不触发条件]

## 使用说明

[详细的使用指南]

## 配置参数

[参数说明]

## 执行流程

[步骤描述]
```

### 关键配置项说明

| 配置项 | 说明 | 是否必需 |
|--------|------|----------|
| Skill 名称 | 唯一标识，用于斜杠命令 | 必需 |
| 描述 | 简要说明 Skill 的作用 | 推荐 |
| TRIGGER | 自动触发的条件 | 可选 |
| templates/ | 输出模板文件 | 可选 |
| references/ | 参考文档和指南 | 可选 |

---

## 实战案例：开发一个代码简化 Skill

接下来，让我们从零开发一个实用的 Skill —— **代码简化审查器**。

### 场景描述

这个 Skill 的作用是：审查代码变更，检查是否有重复代码、可复用的模式、效率问题，并给出修复建议。

### 实现步骤

**步骤 1：创建目录结构**

```bash
mkdir -p .claude/skills/simplify/templates
mkdir -p .claude/skills/simplify/references
```

**步骤 2：编写 SKILL.md 主配置**

```markdown
# simplify

代码简化审查器 - 检查代码变更中的重复模式、可复用性和效率问题。

## 触发方式

- 斜杠命令：`/simplify`
- 自动触发：当用户请求"简化代码"、"代码审查"、"检查重复"时

## 功能说明

审查已变更的代码，输出以下内容：

1. **重复代码检测**：识别相似的代码模式
2. **可复用性分析**：发现可抽象的公共逻辑
3. **效率问题**：检查性能瓶颈和优化空间
4. **修复建议**：给出具体的改进方案

## 输出格式

使用 templates/report.md 模板输出审查报告。
```

**步骤 3：创建输出模板**

`templates/report.md`:

```markdown
# 代码简化审查报告

## 审查概览

- 审查文件数：{count}
- 发现问题数：{issue_count}
- 严重程度：{severity}

## 问题详情

### {issue_type}

**位置**：`{file_path}:{line_number}`

**问题描述**：{description}

**当前代码**：
```
{current_code}
```

**建议修改**：
```
{suggested_code}
```

**收益**：{benefit}

---

## 总结

{summary}
```

**步骤 4：添加参考指南**

`references/principles.md`:

```markdown
# 代码简化原则

## DRY 原则

不要重复自己 - 相同的代码逻辑应该被抽象和复用。

## KISS 原则

保持简单 - 选择最直接、最易懂的实现方式。

## SOLID 原则

遵循面向对象设计的基本原则，确保代码的可维护性。
```

**步骤 5：验证 Skill**

创建完成后，重启 Claude Code 或执行 `/simplify` 测试是否正常工作。

### 运行效果

```bash
# 触发 Skill
/simplify

# 预期输出
正在审查代码变更...

# 代码简化审查报告

## 审查概览
- 审查文件数：3
- 发现问题数：2
- 严重程度：中等

## 问题详情

### 重复代码检测

**位置**：`src/utils.ts:45`

**问题描述**：发现相似的 API 调用模式重复出现 3 次

**当前代码**：
```typescript
// 重复模式 1
fetch('/api/users', { method: 'GET' })
  .then(res => res.json())
  .catch(err => console.error(err));

// 重复模式 2
fetch('/api/posts', { method: 'GET' })
  .then(res => res.json())
  .catch(err => console.error(err));
```

**建议修改**：
```typescript
async function fetchData<T>(url: string): Promise<T> {
  const res = await fetch(url);
  return res.json();
}

// 使用
const users = await fetchData<User[]>('/api/users');
const posts = await fetchData<Post[]>('/api/posts');
```

**收益**：减少 60% 的代码量，统一错误处理逻辑
```

---

## 进阶技巧

### 技巧一：使用 TRIGGER 实现自动触发

当你的 Skill 需要在特定场景自动激活时，使用 TRIGGER 条件：

```markdown
## 触发条件

TRIGGER when: code imports `react` or `vue`, or user asks about frontend component patterns
DO NOT TRIGGER when: code imports `express` or `koa`, or backend API development
```

### 技巧二：模板变量占位

在模板中使用 `{variable}` 语法定义变量，Skill 执行时会自动填充：

```markdown
# 审查报告

**项目**：{project_name}
**日期**：{current_date}
**审查人**：{reviewer}
```

### 技巧三：引用外部文档

将详细的规范文档放在 `references/` 目录，在 SKILL.md 中引用：

```markdown
## 执行规范

请严格按照 references/style-guide.md 中定义的代码规范进行审查。
```

### 技巧四：组合多个 Skill

复杂场景可以拆分成多个 Skill，按需调用：

```
skills/
├── code-review/      # 代码审查
├── test-gen/         # 测试生成
├── doc-gen/          # 文档生成
└── commit/           # 提交规范
```

---

## 注意事项

- ⚠️ **TRIGGER 条件要精确**：过于宽泛的条件可能导致 Skill 在不合适的场景被触发
- ⚠️ **模板要有边界**：明确 Skill 的适用范围，不要试图做一个"万能"的 Skill
- ⚠️ **版本控制**：将 `.claude/skills/` 目录纳入 Git 管理，方便团队共享
- ⚠️ **命名规范**：使用小写字母和连字符，如 `code-review`、`test-gen`
- ⚠️ **性能考虑**：避免在 Skill 中加载过大的参考文档，影响响应速度

---

## 总结

本文介绍了 Claude Skill 的核心概念和完整开发流程：

| 知识点 | 说明 |
|--------|------|
| Skill 定义 | 可复用的提示词模板，定义 AI 的行为模式 |
| 目录结构 | SKILL.md + templates/ + references/ |
| 触发方式 | 斜杠命令 `/skill-name` 或自动触发 |
| 开发流程 | 创建目录 → 编写配置 → 添加模板 → 验证测试 |
| 最佳实践 | 精确触发条件、明确边界、版本控制、规范命名 |

## 参考资料

- [Claude Code 官方文档](https://docs.anthropic.com/claude-code)
- [Skill 开发指南](https://docs.anthropic.com/claude-code/skills)

## 互动交流

你在使用 Claude Skill 时有什么心得？开发了哪些有意思的 Skill？欢迎分享交流！