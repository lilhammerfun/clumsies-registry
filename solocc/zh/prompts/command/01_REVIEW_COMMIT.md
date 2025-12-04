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
   - 确定影响范围（scope）
   - 编写简洁准确的描述（subject）
   - 如需要，编写详细说明（body）

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
