# AI 开发标准 全体说明

> **版本**：v0.1（试行版）  
> **最后更新**：2026-08-20  
> **读者**：第一次接触本标准的开发者、项目负责人、审查者  
> **可单独阅读**：无需 clone 仓库，仅阅读本文件即可了解全貌。详细模板见文末链接。

---

## 1. 这套标准是什么

**AI Engineering Playbook**（以下简称「Playbook」）是公司内部的 **AI 辅助开发标准**。

- **给人看的规则**：开发流程、设计阶段划分、命名、Git、Review 原则
- **给 AI 用的工具**：提示词、输出格式（契约）、验收检查清单、任务卡
- **在项目中的用法**：将模板复制到各项目的 `docs/`，AI 与开发者基于同一前提协作

Playbook 本身是 **存放标准的仓库**，实际应用代码在 `interview-management` 等各项目仓库中。

**标准仓库**：https://github.com/zhoukai2xxx/ai-engineering-playbook

---

## 2. 为什么需要

| 问题 | 标准如何帮助 |
|------|--------------|
| 各人用 Cursor 的方式不一致 | 统一 Ask / Agent 分工与「必须人工确认」的边界 |
| 需求、设计、实现交接模糊 | 固定 KICKOFF → REQUIREMENTS → 设计 → 任务拆分的顺序 |
| AI 输出质量随对话波动 | 用提示词、输出契约、检查清单固定输入/输出 |
| 重复踩坑 | 项目结束后将经验回收到 Playbook |

**第一个试点项目**：`interview-management`（面试管理系统）。Playbook 内 `06-reference-projects/interview-management/` 持续积累实践经验。

---

## 3. 与相关仓库的关系

| 仓库 | 角色 | 说明 |
|------|------|------|
| **ai-engineering-playbook** | 开发标准、AI 工作流、模板 | 本说明的正本 |
| **company-databases** | 统一管理各项目 DB Schema | 按项目分目录 |
| **interview-management** 等 | 实际业务系统代码 | 各系统独立 Git 仓库 |
| **employee-info-management** | 现有 OA 系统 | 逐步向标准靠拢 |

```
[ ai-engineering-playbook ]  ← 标准、模板、提示词
         ↓ 复制、引用
[ 各项目 /docs/ ]            ← KICKOFF、REQUIREMENTS、设计文档
         ↓
[ 各项目代码 ]               ← 实现
         ↓ Schema 共享
[ company-databases ]        ← DB 定义的单一参照源
```

---

## 4. 谁该读什么

| 读者 | 先读 | 再读 |
|------|------|------|
| **项目负责人** | 本文件 → [core-five](https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/00-governance/core-five.md) | [AI 协作原则](https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/00-governance/ai-collaboration-policy.md) |
| **开发者** | 本文件 → [任务卡](https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/04-ai-workflows/task-templates/task-card-template.md) | 负责阶段的 prompts（`04-ai-workflows/prompts/`） |
| **审查者** | [验收检查清单](https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/04-ai-workflows/acceptance-checklists/) | [输出契约](https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/04-ai-workflows/output-contracts/) |

**预计用时**：本文件 5–10 分钟；动手前再花 5 分钟读 [core-five](https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/00-governance/core-five.md)。

---

## 5. 新项目流程（全貌）

遵循日本 IT 行业常见的设计阶段划分，各阶段均为 **AI 起草 → 人工确认**。

```
项目启动 (KICKOFF.md)
  ↓
需求定义 (REQUIREMENTS.md)     ← AI 辅助 + 人工确认【必须】
  ↓
基本设计 (BASIC-DESIGN.md)     ← AI 辅助 + 人工确认
  ↓
详细设计 (DETAILED-DESIGN.md)  ← API / DB / 画面 + 人工确认
  ↓
环境搭建 (SETUP.md)
  ↓
任务拆分（任务卡）              ← AI 辅助
  ↓
各 Phase 实现                   ← Ask 定方案 → Agent 实现 + Review
  ↓
测试                            ← AI 辅助（用例/脚本）+ 人工确认
  ↓
部署                            ← 人工主导（清单可 AI 起草）
  ↓
经验回收 → 06-reference-projects/  ← AI 辅助起草 + 人工筛选入库
```

| 阶段 | 产出 | Playbook 内模板 |
|------|------|-----------------|
| 0 启动 | KICKOFF.md | `05-templates/project-kickoff-template.md` |
| 1 需求 | REQUIREMENTS.md | `05-templates/requirements-template.md` |
| 2 基本设计 | BASIC-DESIGN.md | `05-templates/basic-design-template.md` |
| 3 详细设计 | DETAILED-DESIGN.md | `05-templates/detailed-design-template.md` |
| 4 环境 | SETUP.md | `05-templates/setup-template.md` |
| 5 实现 | 代码 | 任务卡 + 实现提示词 |
| 6 测试 | 测试用例 / 测试代码 | 验收检查清单 + AI 辅助 |
| 7 部署 | 部署与上线 | 人工主导；检查清单可 AI 起草 |
| 8 回收 | lessons-learned 等 | `06-reference-projects/`（AI 起草 + 人工筛选） |

**未通过验收的 AI 输出，不得进入下一阶段。**

---

## 6. AI（Cursor）用法（最低限度）

### 6.1 基本原则

1. **AI 起草，人决策**：范围、权限、DB、生产配置由人确定  
2. **固定输入/输出**：使用 Playbook 中的提示词与输出契约，避免临时拼凑  
3. **小步推进**：不要一次把整个 Phase 交给 AI，以任务卡为单位推进  
4. **新对话开头**：让 AI 先读 `docs/KICKOFF.md` 与 `docs/REQUIREMENTS.md`  

### 6.2 Ask 与 Agent

| 模式 | 适用场景 |
|------|----------|
| **Ask** | 方案咨询、对比、代码理解、Review、需求/设计的 Markdown 初稿 |
| **Agent** | 设计确定后的实现、创建/修改文件、执行命令 |

**推荐**：Ask 达成一致 → 任务卡明确范围 → Agent 执行。

| 判断 | 条件 |
|------|------|
| **先出方案（Ask）** | 新模块、权限、DB、外部对接、跨多文件变更 |
| **直接写代码（Agent）** | 设计已确定、范围清晰、仅 1–2 个文件 |

### 6.3 必须人工确认

- 需求范围（做什么 / 不做什么）
- 权限模型
- DB Schema 变更（与 `company-databases` 一致）
- API 契约定稿
- 生产部署配置与密钥
- 外部系统（OA 等）对接方式
- UI/UX 最终决策

### 6.4 AI 不得自行决定

- 生产环境的 API Key、密码、连接字符串
- 数据删除等不可逆操作
- 擅自更换技术栈（遵循 Playbook 标准）
- 修改现有 OA 核心逻辑（无明确指令时）

---

## 7. 核心五点（A–E）概要

日常开发 **每次都要用的最小集合**。细则以各文件为准。

| | 内容 | Playbook 路径 |
|--|------|---------------|
| **A** | AI 协作原则（Ask/Agent、人工确认边界） | `00-governance/ai-collaboration-policy.md` |
| **B** | 任务拆分（任务卡 + 拆分提示词） | `04-ai-workflows/task-templates/` |
| **C** | 输出契约（AI 必须遵守的章节结构） | `04-ai-workflows/output-contracts/` |
| **D** | 项目启动（KICKOFF 模板） | `05-templates/project-kickoff-template.md` |
| **E** | 经验回收（lessons / patterns / mistakes） | `06-reference-projects/` |

**记忆**：A 守规则 → D 启动项目 → B+C 交给 AI → E 留给下一个项目。

---

## 8. 多人协作时

| 事项 | 规则 |
|------|------|
| **DB** | Schema 在 `company-databases` 共享；变更由指定负责人 Review 后合并 |
| **任务** | 统一任务卡格式（目的、范围、不做的事、验收标准） |
| **API / DB 变更** | 人确定后再实现，勿直接合并 AI 草案 |
| **Git** | `main` 保持稳定；功能分支 `feature/<phase>-<description>`；commit 格式 `[Phase X] 说明` |
| **合并** | 各自 feature 分支 → Review → 合并 |

---

## 9. 技术栈（标准）

| 层 | 首选 | 现有项目替代 |
|----|------|--------------|
| 全栈 Web | Next.js + TypeScript | — |
| 前端 SPA | React + Vite + TypeScript | Bootstrap |
| 后端 API | Next.js API Routes | Spring Boot（Java） |
| DB | PostgreSQL | — |
| ORM | Prisma | Flyway（Java） |
| 样式 | Tailwind CSS | Bootstrap |
| 部署 | AWS EC2 + Docker Compose | — |
| AI 辅助 | Cursor | — |

新项目原则上采用 **首选** 方案；现有系统不必强行重写，从改动部分逐步靠拢标准。

---

## 10. 常见问题

**Q. Playbook 里所有文件都要填完吗？**  
A. 不必。**核心五点（A–E）** 加上项目的 `docs/KICKOFF.md`、`REQUIREMENTS.md` 即可起步。未完成的章节会陆续补充（v0.1 为试行版）。

**Q. 现有项目能用吗？**  
A. 可以。新功能只引入任务卡与 AI 协作原则、事后补设计文档等，均可分阶段导入。

**Q. 只有日语吗？**  
A. Playbook 正文以 **日语** 为正本。中文全体说明即本文件；日语版见 `docs/AI開発標準_全体説明.md`。

**Q. 可以只发这一份文件给别人吗？**  
A. 可以。先分享整体认知，达成一致后再提供 Playbook 链接或 clone，这是预期用法。

**Q. 和 README 有什么区别？**  
A. 本文件面向 **第一次听说标准的人**；README 是仓库索引；core-five 是 **开始干活时的最短步骤**。

---

## 11. 延伸阅读（链接）

| 用途 | URL |
|------|-----|
| 仓库首页 | https://github.com/zhoukai2xxx/ai-engineering-playbook |
| README（索引） | https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/README.md |
| 核心五点 | https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/00-governance/core-five.md |
| AI 协作原则 | https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/00-governance/ai-collaboration-policy.md |
| 开发总则 | https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/00-governance/development-policy.md |
| 项目生命周期 | https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/01-project-lifecycle/README.md |
| 任务卡 | https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/04-ai-workflows/task-templates/task-card-template.md |
| 验收检查清单 | https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/04-ai-workflows/acceptance-checklists/ |
| KICKOFF 模板 | https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/05-templates/project-kickoff-template.md |
| 需求模板 | https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/05-templates/requirements-template.md |
| 参考项目（面试管理） | https://github.com/zhoukai2xxx/ai-engineering-playbook/tree/main/06-reference-projects/interview-management |
| 日语版全体说明 | https://github.com/zhoukai2xxx/ai-engineering-playbook/blob/main/docs/AI開発標準_全体説明.md |

---

*本文为 AI Engineering Playbook 的概要。模板、提示词、检查清单的最新版以上述仓库为准。*
