# rpiv-loop

RPIV 四阶段开发流程插件，为 Claude Code 提供结构化、可追溯的功能开发工作流。

## 安装

```bash
claude plugin add /path/to/rpiv-loop
```

或将本目录发布为独立仓库后：

```bash
claude plugin add github:zqx/rpiv-loop
```

## RPIV 是什么

RPIV 将功能开发分为四个阶段：

| 阶段 | 含义 | 核心问题 |
|------|------|---------|
| **R** - Requirements | 需求 | 做什么？为什么做？ |
| **P** - Plan | 计划 | 怎么做？按什么顺序？ |
| **I** - Implement | 实施 | 把计划变成代码 |
| **V** - Validate | 验证 | 做得对不对？好不好？ |

## 命令总览

### 核心流程

| 命令 | 阶段 | 说明 |
|------|------|------|
| `/rpiv_loop:brainstorm` | R 前 | 通过访谈对话澄清产品需求 |
| `/rpiv_loop:create-prd` | R | 基于对话上下文生成产品需求文档 |
| `/rpiv_loop:plan-feature` | P | 深入代码库分析，创建全面的实施计划 |
| `/rpiv_loop:execute` | I | 按计划逐步实施，边做边验证 |
| `/rpiv_loop:validation:code-review` | V | 技术代码审查 |
| `/rpiv_loop:validation:execution-report` | V | 生成实施报告 |
| `/rpiv_loop:validation:system-review` | V | 流程级元分析 |
| `/rpiv_loop:validation:code-review-fix` | V | 修复审查发现的问题 |
| `/rpiv_loop:validation:validate` | V | 自动检测项目类型并运行验证 |

### 辅助工具

| 命令 | 说明 |
|------|------|
| `/rpiv_loop:prime` | 加载项目上下文 |
| `/rpiv_loop:record` | 记录问题/需求/待办 |
| `/rpiv_loop:fix` | 处理 todo 条目 |
| `/rpiv_loop:flow-status` | 查看过程文件状态 |
| `/rpiv_loop:archive` | 归档已完成文件 |

### 自动化

| 命令 | 说明 |
|------|------|
| `/rpiv_loop:biubiubiu` | 全自主 agent 团队，一键完成 R→P→I→V |

## 典型工作流

### 标准流程（推荐）

```
brainstorm → create-prd → plan-feature → execute → code-review → execution-report → system-review → archive
```

每个阶段之间建议 `/clear` 清理上下文，保持 AI 专注。

### 快速流程（小功能）

跳过 brainstorm 和部分验证：

```
create-prd → plan-feature → execute → code-review
```

### 全自动流程

brainstorm 完成后，一键启动 agent 团队：

```
brainstorm → biubiubiu
```

## 过程文件目录

插件使用的过程文件存放在项目根目录的 `rpiv/` 下：

```
rpiv/
├── requirements/          # PRD 文档
├── plans/                 # 实施计划
├── validation/            # 验证报告（code-review / exec-report / system-review）
├── todo/                  # 待办条目（issue / feature / todo）
└── archive/               # 已归档文件
```

所有过程文件包含 YAML frontmatter，用于状态追踪（`pending` → `in-progress` → `completed` → `archived`）。

## 方法论

详细的 RPIV 方法论说明请参考 `skills/rpiv-methodology/SKILL.md`。
