# Git Commit 规范

## 格式

```
<type>: <总结>

<修改原因>

- 核心修改1
- 核心修改2
- 核心修改3
```

## Type选择

**单一类型**：`feat`, `fix`, `refactor`, `perf`, `docs`, `style`, `test`, `chore`

**混合类型**（包含多种修改）：选最能代表核心变更的
- `refactor`: 架构调整、数据模型变更为主
- `feat`: 新增功能为主
- `improve`: 整体改进

## 原理

- **标题**：说明改了什么（50字符内）
- **原因**：说明为什么改（一句话，大改动建议加，小改动可省略）
- **列表**：按重要性排序，前面是核心业务逻辑，后面是技术细节

## 禁止

❌ 文件统计、测试结果、时间、性能数字、个人想法

## 示例

**大改动（需要原因）**：
```
refactor: migrate to reserve-based pricing

Price should be derived from reserves, not stored separately.

- Add init trade insertion with reserves from IDOCreated event
- Update indexer to record reserve_usdc and reserve_tokens
- Update query services to calculate price from reserves on-the-fly
- Optimize Docker build with cargo-chef
- Sync contract ABIs
```

**小改动（不需要原因）**：
```
chore: update contract addresses

- Update Factory address in .env
- Update implementation addresses
- Sync ABIs with deployed contracts
```

## AI 署名

当 commit 由 AI Agent 生成时，需要在末尾添加署名：

```
🤖 Generated with [Claude Code](https://claude.com/claude-code)

Co-Authored-By: Claude <model-name> <noreply@anthropic.com>
```

将 `<model-name>` 替换为实际模型名（如 `Opus 4.5`、`Sonnet 4`）。
