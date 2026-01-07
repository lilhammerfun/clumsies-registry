# Claude Agent - Prompts 体系

> 通用的 AI Agent 提示词体系，指导 Claude Code 的行为规范。

## 一、Prompts 体系

本体系使用 `.prompts/` 目录组织所有 AI Agent 相关文档。

### 1.1 目录结构

```
project-root/
├── CLAUDE.md                    # 入口文件（本文件）
└── .prompts/
    ├── biz/                     # 业务上下文
    │   ├── OVERVIEW.md          # 业务概览
    │   └── {module}/            # 按模块组织的业务文档
    ├── tech/                    # 技术上下文
    │   └── {project}/           # 按项目组织的技术文档
    ├── conduct/                 # 通用开发规范
    │   ├── CODE_COMMENTS.md     # 代码注释规范
    │   ├── DEPENDENCIES.md      # 依赖管理
    │   ├── TESTING.md           # 测试要求
    │   ├── COMPATIBILITY.md     # 向后兼容原则
    │   ├── GIT_COMMIT.md        # Git 提交消息规范
    │   └── GIT_OPERATIONS.md    # Git 操作权限
    └── command/                 # 自定义指令
        ├── 00_CONTEXT_REINFORCEMENT.md
        └── 01_REVIEW_COMMIT.md
```

### 1.2 目录说明

| 目录 | 作用 | 内容示例 |
|------|------|---------|
| `biz/` | 业务上下文 | 产品逻辑、业务流程、领域模型 |
| `tech/` | 技术上下文 | 架构设计、技术栈、API 文档 |
| `conduct/` | 开发规范 | 代码风格、Git 规范、测试要求 |
| `command/` | 自定义指令 | 可复用的任务流程 |

### 1.3 文件命名规范

- **文档文件**：全大写 SNAKE_CASE
  - 示例：`OVERVIEW.md`, `CODE_COMMENTS.md`, `GIT_COMMIT.md`
  - 原因：文件名自文档化，醒目易识别

- **指令文件**：序号前缀 + 全大写 SNAKE_CASE
  - 示例：`00_CONTEXT_REINFORCEMENT.md`, `01_REVIEW_COMMIT.md`
  - 原因：序号便于快速引用（"执行指令0"）
  - 特殊：`00` 开头通常是系统级/元级指令

- **目录**：小写 kebab-case
  - 示例：`biz/`, `tech/`, `conduct/`, `command/`

- **不使用 README.md**：文件名应直接说明内容，避免冗余索引

---

## 二、自定义指令系统

### 2.1 目的

为频繁执行的任务定义可复用的指令流程。

### 2.2 指令文件格式

```markdown
# 指令名称

## 描述
简要说明这个指令的作用

## 执行步骤
1. 第一步操作
2. 第二步操作
3. ...

## 注意事项
- 需要遵守的规范
- 特殊约束条件
```

### 2.3 使用方式

用户可以通过以下方式执行指令：
- **通过序号**："执行指令0" → 读取 `.prompts/command/00_*.md`
- **通过名称**："执行 REVIEW_COMMIT" → 读取对应指令文件
- Agent 按照文档定义的步骤执行任务

### 2.4 内置指令

| 序号 | 名称 | 作用 |
|------|------|------|
| 00 | CONTEXT_REINFORCEMENT | 上下文加强，重新检阅文档并纠正错误 |
| 01 | REVIEW_COMMIT | 检查 git 修改并生成 commit message |

---

## 三、文档使用原则

### 3.1 阅读顺序

在开始任何开发工作前，**必须**阅读相关文档：

1. `CLAUDE.md`（本文档）→ 了解准则和规范
2. `.prompts/biz/` → 理解业务逻辑
3. `.prompts/tech/{项目名}/` → 项目技术文档
4. `.prompts/conduct/` → 通用开发规范

### 3.2 文档优先开发

- 如果用户需求涉及**业务逻辑变更** → 先更新 `biz/` 下的文档
- 如果用户需求涉及**技术方案变更** → 先更新 `tech/` 下的文档
- **先更新文档，再开始开发**

### 3.3 文档保持最新

- 文档只记录**当前版本**，不记录历史变更
- 新需求/设计加入时，移除对应的旧内容
- 历史变更由 Git 记录

---

## 四、Agent 行为准则

### 4.1 语言要求

根据项目配置，遵循特定的语言使用规范：
- **回答问题和思考过程**：使用项目配置的首选语言（默认中文）
- **代码和注释**：使用英文（国际惯例）
- **Git commit message**：使用英文（开源社区惯例）

### 4.2 开发规范

具体的开发规范请参考 `.prompts/conduct/` 目录：
- `CODE_COMMENTS.md` — 代码注释规范
- `DEPENDENCIES.md` — 依赖管理
- `TESTING.md` — 测试要求
- `COMPATIBILITY.md` — 向后兼容原则
- `GIT_COMMIT.md` — Git 提交消息规范
- `GIT_OPERATIONS.md` — Git 操作权限

---

## 五、执行优先级

当出现冲突时，按以下优先级处理：

1. **CLAUDE.md**（本文档）— 最高准则
2. **conduct/** — 开发行为规范
3. **biz/** — 业务逻辑理解
4. **tech/** — 项目技术文档
5. **用户指令** — 具体任务需求

优先级高的覆盖优先级低的。

---

## 六、扩展指南

根据项目需要，可以添加以下目录：

- `.prompts/biz/` — 业务逻辑文档
- `.prompts/tech/` — 项目技术文档

---

**记住：所有规则、规范和上下文都在 `.prompts/` 目录中。**
