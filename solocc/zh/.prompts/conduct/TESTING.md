# 测试要求

**原则**：通过自动化测试验证代码，不通过启动服务检查bug。

## 后端和合约项目

通过编写集成测试验证代码：
```bash
# 合约测试
forge test

# 后端测试
cargo test
```

## 前端项目

通过编译检查（lint）验证代码：
```bash
# 类型检查
pnpm exec tsc --noEmit

# Lint检查
pnpm run lint
```

## 禁止的测试方式

❌ 启动开发服务器检查bug：
```bash
# 禁止使用这种方式确认代码是否有bug
pnpm run dev
cargo run
```
