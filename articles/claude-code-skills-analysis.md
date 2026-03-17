# 深度解析 Claude Code：GitHub 上 10 个顶级 Skills 的设计亮点与实战指南

## 引言

Claude Code 的 Skills 生态在过去一年爆发式增长。从 Manus 工作流到安全审计，从内容人性化到一键部署，社区贡献了数百个高质量 Skills。

**哪些 Skills 真正值得你的时间？**

本文基于 GitHub Star 数据，精选了 10 个最受欢迎的 Claude Code Skills，深入分析它们的设计亮点、安装方法和使用场景。

## 内容概览

| Skill | Stars | 核心功能 | 项目地址 |
|-------|-------|----------|----------|
| planning-with-files | 16.2k | Manus 工作流实现 | [GitHub](https://github.com/OthmanAdi/planning-with-files) |
| awesome-agent-skills | 11.5k | 500+ Skills 精选 | [GitHub](https://github.com/VoltAgent/awesome-agent-skills) |
| humanizer | 9.6k | 消除 AI 写作痕迹 | [GitHub](https://github.com/blader/humanizer) |
| claude-skills | 5.4k | 192 个生产级 Skills | [GitHub](https://github.com/alirezarezvani/claude-skills) |
| Humanizer-zh | 4.9k | Humanizer 中文版 | [GitHub](https://github.com/op7418/Humanizer-zh) |
| trailofbits/skills | 3.6k | 安全审计工具集 | [GitHub](https://github.com/trailofbits/skills) |
| pinme | 3.0k | 一键部署前端 | [GitHub](https://github.com/glitternetwork/pinme) |
| videocut-skills | 1.1k | 视频剪辑 Agent | [GitHub](https://github.com/Ceeon/videocut-skills) |
| android-re-skill | 974 | Android 逆向工程 | [GitHub](https://github.com/SimoneAvogadro/android-reverse-engineering-skill) |
| skill-codex | 874 | Codex 集成 | [GitHub](https://github.com/skills-directory/skill-codex) |

---

## Skill 一：planning-with-files — Manus 工作流的「开源实现」

### 项目地址

**GitHub**: https://github.com/OthmanAdi/planning-with-files

**Stars**: 16,262 ⭐

### 核心定位

这个 Skill 实现了 Manus 的持久化 Markdown 计划工作流——正是 Meta 以 20 亿美元收购的那家 AI Agent 公司的核心方法论。

### 设计亮点

**亮点一：持久化计划系统**

```
.planning/
├── plan.md          # 当前计划状态
├── tasks.md         # 任务清单
└── memory/          # 上下文记忆
```

所有计划都以 Markdown 文件形式存储，即使上下文清空也能恢复。

**亮点二：Session Recovery**

当你的 Claude Code 上下文满了需要 `/clear` 时：

1. 自动检测之前的会话数据
2. 找到计划文件最后更新时间
3. 提取可能丢失的对话内容
4. 生成恢复报告

**亮点三：多平台支持**

支持 16 个 AI 编程工具：

| 平台 | 支持程度 |
|------|----------|
| Claude Code | ✅ 完整支持 |
| Gemini CLI | ✅ 完整支持 |
| Cursor | ✅ 完整支持 |
| Codex | ✅ 完整支持 |
| GitHub Copilot | ✅ 支持（v2.16.0+） |

**亮点四：社区 Fork 生态**

社区已经基于它创建了多个变体：

- [devis](https://github.com/st01cs/devis) - 面试优先工作流
- [multi-manus-planning](https://github.com/kmichels/multi-manus-planning) - 多项目支持
- [plan-cascade](https://github.com/Taoidle/plan-cascade) - 多级任务编排

### 安装方法

**Claude Code**:

```bash
# 添加为 marketplace
/plugin marketplace add OthmanAdi/planning-with-files

# 或克隆到本地
git clone https://github.com/OthmanAdi/planning-with-files.git
# 复制 .claude/ 目录到你的项目
```

**Codex**:

```bash
git clone https://github.com/OthmanAdi/planning-with-files.git ~/.codex/planning-with-files
```

### 使用方法

```bash
# 开始规划
/planning-with-files

# 查看状态
/plan:status

# 恢复会话
/clear  # 自动触发恢复
```

### 核心价值

- **方法论落地**：把 20 亿美元收购的工作流开源
- **上下文不丢失**：持久化存储 + 会话恢复
- **社区活跃**：持续更新，有大量 Fork 变体

---

## Skill 二：awesome-agent-skills — 500+ Skills 的「官方精选」

### 项目地址

**GitHub**: https://github.com/VoltAgent/awesome-agent-skills

**Stars**: 11,530 ⭐

### 核心定位

这不是一个 Skill，而是一个 Skills 索引库。收录了 Anthropic、Google Labs、Vercel、Stripe、Cloudflare、Netlify 等顶级团队的官方 Skills。

### 设计亮点

**亮点一：官方团队贡献**

收录了来自顶级公司的官方 Skills：

| 来源 | 代表 Skills |
|------|-------------|
| Anthropic | docx, pptx, xlsx, pdf, mcp-builder |
| Stripe | stripe-best-practices, upgrade-stripe |
| Expo | expo-app-design, expo-deployment |
| Supabase | postgres-best-practices |
| Google Gemini | gemini-skills |
| HashiCorp | terraform-code-generation |

**亮点二：多工具兼容**

所有 Skills 都兼容：

- Claude Code
- OpenAI Codex
- Gemini CLI
- Cursor
- GitHub Copilot
- Windsurf
- OpenCode

**亮点三：质量筛选标准**

不同于批量生成的 Skills 仓库，这个合集专注于：

> "real-world Agent Skills created and used by actual engineering teams, not mass AI-generated stuff."

**亮点四：安全提醒**

明确标注了使用 Skills 的安全风险，推荐安全扫描工具：

- [Snyk Skill Security Scanner](https://github.com/snyk/agent-scan)
- [Agent Trust Hub](https://ai.gendigital.com/agent-trust-hub)

### 安装方法

这是一个索引库，你需要根据每个 Skill 的链接单独安装：

```bash
# 示例：安装 Anthropic 官方 docx Skill
git clone https://github.com/anthropics/skills.git
# 复制 skills/docx 到 ~/.claude/skills/
```

### 使用方法

作为参考目录使用：

1. 浏览 [awesome-agent-skills](https://github.com/VoltAgent/awesome-agent-skills)
2. 找到你需要的 Skill
3. 点击链接跳转到对应仓库
4. 按该仓库的说明安装

### 核心价值

- **官方权威**：收录顶级团队的官方 Skills
- **质量保证**：筛选真实团队使用的 Skills
- **一站式发现**：不用到处搜索，一个仓库搞定

---

## Skill 三：humanizer — 消除 AI 写作痕迹的「文本净化器」

### 项目地址

**GitHub**: https://github.com/blader/humanizer

**Stars**: 9,626 ⭐

### 核心定位

识别并消除文本中 AI 生成的痕迹，让内容听起来更自然、更像人类写的。

### 设计亮点

**亮点一：基于 Wikipedia 的 AI 写作指南**

这个 Skill 基于 Wikipedia 的 "[Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing)" 页面，由 WikiProject AI Cleanup 维护。

**亮点二：24 种 AI 写作模式检测**

| 类别 | 检测模式 |
|------|----------|
| 内容模式 | 过度强调意义、推广性语言、-ing 分析、模糊归因 |
| 语言模式 | AI 高频词、is/are 回避、否定平行、三段式 |
| 风格模式 | 破折号滥用、粗体滥用、标题大小写、emoji 滥用 |
| 沟通模式 | 协作性用语、知识截止免责、讨好语气 |

**亮点三：「注入灵魂」机制**

不只是删除 AI 模式，还会：

1. **有观点**：不要中性报道，要有态度
2. **变化节奏**：短句长句交替
3. **承认复杂**：承认不确定和矛盾
4. **使用"我"**：第一人称增加真实感
5. **允许混乱**：旁枝末节、半成形想法更人类

**亮点四：两轮修订流程**

```
原文 → 初稿改写 → AI 痕迹审计 → 最终版本
```

第二步会问："What makes the below so obviously AI generated?"，找出剩余问题。

### 安装方法

```bash
# 克隆仓库
git clone https://github.com/blader/humanizer.git

# 复制到 Claude Code skills 目录
cp -r humanizer ~/.claude/skills/
```

### 使用方法

```bash
# 在 Claude Code 中
/humanizer [你的文本]

# 或直接让 Claude 处理
"请用 humanizer 技能帮我优化这段文字"
```

### 核心价值

- **基于权威指南**：Wikipedia 维护的检测模式
- **不只是删除**：注入真实的写作风格
- **实用性强**：对于内容创作者、营销人员极有价值

---

## Skill 四：claude-skills — 192 个生产级 Skills 的「瑞士军刀」

### 项目地址

**GitHub**: https://github.com/alirezarezvani/claude-skills

**Stars**: 5,443 ⭐

### 核心定位

最全面的开源 Skills 库，包含 192 个生产就绪的 Skills，覆盖工程、营销、产品、合规、C 级顾问等 9 大领域。

### 设计亮点

**亮点一：9 大领域覆盖**

| 领域 | Skills 数量 | 示例 |
|------|-------------|------|
| 工程核心 | 24 | security-auditor, playwright-pro |
| 高级工程 | 25 | POWERFUL 级别 Skills |
| 产品 | 12 | product-manager, user-research |
| 营销 | 43 | content-creator, seo-optimizer |
| 监管/质量 | 12 | compliance-checker, qa-reviewer |
| 项目管理 | 6 | sprint-planner, risk-assessor |
| C 级顾问 | 28 | CEO, CTO, CFO 等视角 |
| 业务增长 | 4 | growth-hacker, partnership |
| 财务 | 2 | financial-analyst, saas-metrics |

**亮点二：Skills / Agents / Personas 三层架构**

| 类型 | 作用 | 示例 |
|------|------|------|
| Skills | 如何执行任务 | "Follow these steps for SEO" |
| Agents | 做什么任务 | "Run a security audit" |
| Personas | 谁在思考 | "Think like a startup CTO" |

三者可以组合使用。

**亮点三：多工具转换**

一个脚本转换为 7 个工具：

```bash
./scripts/convert.sh --tool all

# 支持：
# Cursor → .mdc rules
# Aider → CONVENTIONS.md
# Kilo Code → .kilocode/rules/
# Windsurf → .windsurf/skills/
# OpenCode → .opencode/skills/
# Augment → .augment/rules/
# Antigravity → ~/.gemini/antigravity/skills/
```

**亮点四：零依赖 Python 工具**

包含 254 个 Python CLI 脚本，全部只用标准库：

```bash
# 无需 pip install
python scripts/some-tool.py
```

### 安装方法

**Claude Code (推荐)**:

```bash
# 添加 marketplace
/plugin marketplace add alirezarezvani/claude-skills

# 按领域安装
/plugin install engineering-skills@claude-code-skills
/plugin install marketing-skills@claude-code-skills
/plugin install c-level-skills@claude-code-skills

# 或安装单个 Skill
/plugin install skill-security-auditor@claude-code-skills
```

**Gemini CLI**:

```bash
git clone https://github.com/alirezarezvani/claude-skills.git
cd claude-skills
./scripts/gemini-install.sh
```

**Codex**:

```bash
npx agent-skills-cli add alirezarezvani/claude-skills --agent codex
```

### 使用方法

```bash
# 激活特定 Skill
> activate_skill(name="senior-architect")

# 组合使用 Skills + Personas
> activate_skill(name="security-auditor")
> activate_persona(name="cto")
```

### 核心价值

- **全面覆盖**：9 大领域，192 个 Skills
- **多工具兼容**：一键转换为 7 个 AI 编程工具
- **生产就绪**：每个 Skill 都经过验证

---

## Skill 五：Humanizer-zh — 中文 AI 文本净化器

### 项目地址

**GitHub**: https://github.com/op7418/Humanizer-zh

**Stars**: 4,866 ⭐

### 核心定位

Humanizer 的中文版本，专门针对中文 AI 写作痕迹进行优化。

### 设计亮点

**亮点一：中文化适配**

针对中文 AI 写作的特有模式：

- 翻译腔调优化
- 中式表达修正
- 中文 AI 高频词检测

**亮点二：保持原项目所有功能**

完整移植了 Humanizer 的 24 种检测模式，适配中文语境。

### 安装方法

```bash
git clone https://github.com/op7418/Humanizer-zh.git
cp -r Humanizer-zh ~/.claude/skills/
```

### 使用方法

```bash
/humanizer-zh [中文文本]
```

### 核心价值

- **中文优化**：专门针对中文 AI 写作痕迹
- **即开即用**：保持 Humanizer 的简洁体验

---

## Skill 六：trailofbits/skills — 安全审计的「专业工具箱」

### 项目地址

**GitHub**: https://github.com/trailofbits/skills

**Stars**: 3,619 ⭐

### 核心定位

Trail of Bits（知名安全公司）官方发布的 Claude Code Skills，专注于安全研究、漏洞检测和审计工作流。

### 设计亮点

**亮点一：智能合约安全**

| Plugin | 功能 |
|--------|------|
| building-secure-contracts | 6 条链的漏洞扫描 |
| entry-point-analyzer | 识别状态修改入口点 |

**亮点二：代码审计**

包含 12 个审计相关插件：

- `differential-review` - 安全聚焦的 diff 审查
- `semgrep-rule-creator` - 创建自定义 Semgrep 规则
- `static-analysis` - CodeQL + Semgrep + SARIF 解析
- `variant-analysis` - 模式分析找相似漏洞

**亮点三：验证工具**

- `constant-time-analysis` - 检测时序侧信道
- `property-based-testing` - 属性测试指导
- `zeroize-audit` - 检测密钥清零遗漏

**亮点四：Trophy Case**

公开了使用这些 Skills 发现的真实漏洞：

| Skill | 发现的漏洞 |
|-------|-----------|
| constant-time-analysis | [ML-DSA 签名时序侧信道](https://github.com/RustCrypto/signatures/pull/1144) |

### 安装方法

**Claude Code Marketplace**:

```bash
/plugin marketplace add trailofbits/skills
/plugin menu
```

**Codex**:

```bash
git clone https://github.com/trailofbits/skills.git ~/.codex/trailofbits-skills
~/.codex/trailofbits-skills/.codex/scripts/install-for-codex.sh
```

### 使用方法

```bash
# 审计智能合约
/building-secure-contracts

# 创建 Semgrep 规则
/semgrep-rule-creator

# 时序分析
/constant-time-analysis
```

### 核心价值

- **专业团队出品**：Trail of Bits 是顶级安全公司
- **覆盖全面**：智能合约、代码审计、恶意软件分析
- **实战验证**：已发现真实漏洞

---

## Skill 七：pinme — 一键部署前端的「零配置神器」

### 项目地址

**GitHub**: https://github.com/glitternetwork/pinme

**Stars**: 3,017 ⭐

### 核心定位

零配置前端部署工具。不需要服务器、不需要账户、不需要设置——一条命令部署静态站点。

### 设计亮点

**亮点一：真正的零配置**

```bash
npm run build
pinme upload dist
# 完成！
```

**亮点二：去中心化存储**

部署到 IPFS/去中心化网络：

- 内容可验证
- 防止静默篡改
- 无需管理服务器

**亮点三：多框架支持**

| 框架 | 构建目录 |
|------|----------|
| Vite/React/Vue | `dist/` |
| Next.js (static) | `out/` |
| Nuxt | `.output/public/` |

**亮点四：AI 集成**

内置 Claude Code Skill，让 AI 自动执行部署：

```markdown
## For AI
This section provides AI-specific instructions for deploying websites using PinMe CLI.
```

### 安装方法

```bash
npm install -g pinme
```

### 使用方法

```bash
# 基本部署
pinme upload dist

# 绑定域名（需 VIP）
pinme bind your-domain.com

# 查看 CLI 帮助
pinme --help
```

### 核心价值

- **极简部署**：从构建到上线只需两条命令
- **去中心化**：内容可验证，防篡改
- **AI 友好**：内置 Skill 让 AI 自动部署

---

## Skill 八：videocut-skills — 视频剪辑的「AI Agent」

### 项目地址

**GitHub**: https://github.com/Ceeon/videocut-skills

**Stars**: 1,145 ⭐

### 核心定位

使用 Claude Code Skills 实现的视频剪辑 Agent，自动化视频处理工作流。

### 设计亮点

**亮点一：AI 驱动视频剪辑**

- 自动剪辑
- 字幕处理
- 片段提取
- 格式转换

**亮点二：Claude Code 原生集成**

作为 Skills 实现，可以：

- 结合其他 Skills 使用
- 在 Claude Code 中直接调用
- 与文件操作、网络请求等工具配合

### 安装方法

```bash
git clone https://github.com/Ceeon/videocut-skills.git
cp -r videocut-skills ~/.claude/skills/
```

### 使用方法

```bash
/videocut --input video.mp4 --output clips/
```

### 核心价值

- **自动化视频处理**：减少重复劳动
- **AI 原生**：充分利用 Claude 的理解能力
- **开源免费**：无需付费视频处理工具

---

## Skill 九：android-reverse-engineering-skill — Android 逆向工程助手

### 项目地址

**GitHub**: https://github.com/SimoneAvogadro/android-reverse-engineering-skill

**Stars**: 974 ⭐

### 核心定位

支持 Android 应用逆向工程的 Claude Code Skill，提供反编译、分析、漏洞发现等功能。

### 设计亮点

**亮点一：逆向工作流支持**

- APK 反编译
- 代码分析
- 权限检查
- 安全评估

**亮点二：与 Claude 深度集成**

利用 Claude 的代码理解能力：

- 解释混淆代码
- 识别敏感操作
- 生成分析报告

### 安装方法

```bash
git clone https://github.com/SimoneAvogadro/android-reverse-engineering-skill.git
cp -r android-reverse-engineering-skill ~/.claude/skills/
```

### 使用方法

```bash
/android-reverse-engineering --apk target.apk
```

### 核心价值

- **专业领域**：填补 Android 逆向的 Skills 空白
- **AI 加速**：利用 Claude 理解复杂代码
- **安全研究**：支持漏洞发现和评估

---

## Skill 十：skill-codex — Codex 集成桥梁

### 项目地址

**GitHub**: https://github.com/skills-directory/skill-codex

**Stars**: 874 ⭐

### 核心定位

将提示委托给 OpenAI Codex 执行的 Claude Code Skill，实现跨 Agent 协作。

### 设计亮点

**亮点一：跨 Agent 委托**

```bash
# 在 Claude Code 中调用 Codex
/skill-codex "实现一个 React 登录组件"
```

**亮点二：优势互补**

| Claude Code 擅长 | Codex 擅长 |
|-----------------|-----------|
| 复杂推理 | 代码生成速度 |
| 长上下文理解 | 特定语言优化 |
| 多工具协作 | 批量操作 |

### 安装方法

```bash
git clone https://github.com/skills-directory/skill-codex.git
cp -r skill-codex ~/.claude/skills/
```

### 使用方法

```bash
/skill-codex [你的提示]
```

### 核心价值

- **跨 Agent 协作**：同时利用多个 AI Agent 的优势
- **灵活切换**：根据任务选择最佳 Agent
- **简单集成**：一行命令调用

---

## 选型指南

根据你的角色和需求，推荐关注的 Skills：

| 角色 | 推荐 Skills | 理由 |
|------|-------------|------|
| 产品经理 | planning-with-files, claude-skills | 结构化工作流 + C-level 视角 |
| 开发者 | trailofbits/skills, claude-skills | 安全审计 + 工程技能包 |
| 内容创作者 | humanizer, Humanizer-zh | 消除 AI 痕迹 |
| DevOps | pinme | 一键部署 |
| 安全研究员 | trailofbits/skills | 专业安全工具集 |
| 多工具用户 | claude-skills, awesome-agent-skills | 多平台兼容 |

---

## 设计模式总结

通过分析这 10 个顶级 Skills，提炼出核心设计模式：

### 模式一：持久化状态

```markdown
.planning/
├── plan.md      # 状态文件
├── tasks.md     # 任务清单
└── memory/      # 上下文记忆
```

**核心思想**：用文件系统存储状态，让 Agent 可以跨会话恢复。

### 模式二：多工具兼容

```bash
./scripts/convert.sh --tool all
# 一套 Skills，七个工具
```

**核心思想**：Skills 应该与工具无关，通过转换脚本适配多平台。

### 模式三：领域深耕

| Skill | 领域 | 深度 |
|-------|------|------|
| humanizer | 内容 | 24 种检测模式 |
| trailofbits/skills | 安全 | 20+ 专业插件 |
| planning-with-files | 工作流 | Manus 方法论完整实现 |

**核心思想**：与其做 100 个浅显的 Skills，不如做 1 个深度解决特定问题的 Skill。

### 模式四：官方权威

| 来源 | Skills 质量 |
|------|-------------|
| Anthropic 官方 | ⭐⭐⭐⭐⭐ |
| 知名公司官方 | ⭐⭐⭐⭐ |
| 社区维护 | ⭐⭐⭐ |

**核心思想**：优先选择官方团队发布的 Skills，质量和维护更有保障。

---

## 参考资料

- [Claude Code 官方文档](https://docs.anthropic.com/claude-code)
- [Anthropic 官方 Skills](https://github.com/anthropics/skills)
- [VoltAgent Awesome Agent Skills](https://github.com/VoltAgent/awesome-agent-skills)

---

你对哪个 Skill 最感兴趣？欢迎在评论区分享你的使用体验！