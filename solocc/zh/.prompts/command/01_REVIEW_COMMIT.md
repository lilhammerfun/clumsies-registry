# Review Commit

## 描述

检查当前git修改，分析改动内容，生成符合项目规范的commit message建议。

## 执行步骤

1. **查看修改状态**
   - 运行 `git status` 查看修改的文件列表
   - 识别修改涉及的模块和范围

2. **查看具体改动**
   - 运行 `git diff` 查看未staged的改动
   - 运行 `git diff --cached` 查看已staged的改动
   - 分析改动的性质（新功能、修复、重构等）

3. **生成commit message**
   - 根据 `conduct/GIT_COMMIT.md` 规范分析改动类型
   - 确定commit类型：feat/fix/refactor/docs/chore等
   - 编写简洁准确的标题（50字符内）
   - 如需要，编写修改原因（一句话）
   - 如需要，编写核心修改列表（按重要性排序）

4. **输出建议**
   - 向用户展示建议的commit message
   - 说明选择该类型和描述的理由
   - 等待用户确认或修改

## 注意事项

- **严禁自动提交**：只生成建议，不执行 `git add` 或 `git commit`
- **遵循规范**：严格遵循 `conduct/GIT_COMMIT.md` 的格式要求
- **使用英文**：commit message 必须使用英文
- **准确性优先**：如果改动复杂，建议用户拆分成多个commit
- **检查敏感信息**：如果发现.env、credentials等敏感文件，警告用户不要提交
- **添加 AI 署名**：commit message 末尾添加 code agent 的贡献署名
- **列表项原则**：
  - 避免教条主义，不要过度细化
  - 合并相关的改动，一个逻辑点一个列表项
  - 示例：❌ 分5条列举删除、移动、更新等细节 → ✅ 合并成一条"Merge X into Y"
  - 简洁优于详尽
- **简单改动判断（CRITICAL）**：
  - **只写标题**的情况：
    - UI调整：移除/添加/调整单个组件，改布局列数等
    - 简单重构：删除unused import，移除单个功能，重命名变量
    - 配置修改：更新1-3个配置项，调整单个参数
    - 单一目的修改：一句话能说清楚的改动
  - **错误示例**：
    - ❌ `fix: restrict to Sepolia\n- Remove mainnet\n- Remove arbitrum\n- Remove base`
    - ❌ `refactor: remove Token Holders\n\nRemoved the card...\nUpdated grid layout...`
  - **正确示例**：
    - ✅ `fix: restrict wallet connection to Sepolia testnet only`
    - ✅ `refactor: remove Token Holders card from Users tab`
    - ✅ `style: adjust header search component layout`
  - **需要列表的情况**：多个模块/多个逻辑点/复杂的因果关系

## 示例输出

**复杂改动（有原因和列表）**：
```
建议的commit message：

fix: correct unit conversion in price calculations

Division by 1e12 should be multiplication in reserve price formula.

- Fix reserve price calculation in ido_service, user_service, token_service
- Update price display to show correct values

🤖 Generated with [Claude Code](https://claude.com/claude-code)

Co-Authored-By: Claude <noreply@anthropic.com>

理由：
类型 'fix'：修复价格计算的bug，影响多个服务
```

**简单改动（只写标题）**：
```
建议的commit message：

fix: restrict wallet connection to Sepolia testnet only

🤖 Generated with [Claude Code](https://claude.com/claude-code)

Co-Authored-By: Claude <noreply@anthropic.com>

理由：
简单配置修改，标题已清晰说明，不需要原因和列表
```
