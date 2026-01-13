# Release

## 描述

为 clumsies 制作新版本发布，包含交叉编译、校验和生成、GitHub Release 创建。

## 前置条件

- 所有改动已 commit 并 push
- 版本号已在 `src/main.zig` 中更新

## 执行步骤

1. **确认版本号**
   ```bash
   grep 'const version' src/main.zig
   ```

2. **创建版本目录**
   ```bash
   mkdir -p zig-out/bin/vX.Y.Z
   ```

3. **交叉编译 4 个平台**
   每次编译后立即复制到版本目录（防止下次编译覆盖）：
   ```bash
   zig build -Doptimize=ReleaseFast -Dtarget=aarch64-macos && cp zig-out/bin/clumsies zig-out/bin/vX.Y.Z/clumsies-darwin-arm64
   zig build -Doptimize=ReleaseFast -Dtarget=x86_64-macos && cp zig-out/bin/clumsies zig-out/bin/vX.Y.Z/clumsies-darwin-x86_64
   zig build -Doptimize=ReleaseFast -Dtarget=aarch64-linux && cp zig-out/bin/clumsies zig-out/bin/vX.Y.Z/clumsies-linux-arm64
   zig build -Doptimize=ReleaseFast -Dtarget=x86_64-linux && cp zig-out/bin/clumsies zig-out/bin/vX.Y.Z/clumsies-linux-x86_64
   ```

4. **生成 checksums.txt**
   ```bash
   cd zig-out/bin/vX.Y.Z
   shasum -a 256 clumsies-* > checksums.txt
   cat checksums.txt
   ```

5. **验证校验和**
   ```bash
   shasum -a 256 -c checksums.txt
   ```
   确保所有文件显示 OK

6. **创建 GitHub Release**
   回到项目根目录执行：
   ```bash
   gh release create vX.Y.Z \
     zig-out/bin/vX.Y.Z/clumsies-darwin-arm64 \
     zig-out/bin/vX.Y.Z/clumsies-darwin-x86_64 \
     zig-out/bin/vX.Y.Z/clumsies-linux-arm64 \
     zig-out/bin/vX.Y.Z/clumsies-linux-x86_64 \
     zig-out/bin/vX.Y.Z/checksums.txt \
     --title "vX.Y.Z" \
     --notes "## What's New

   - 功能1
   - 功能2

   ## Checksums (SHA256)

   \`\`\`
   <粘贴 checksums.txt 内容>
   \`\`\`"
   ```

7. **验证发布**
   - 打开返回的 GitHub Release URL
   - 确认所有 5 个文件已上传

## 注意事项

- **目录结构**：`zig-out/bin/vX.Y.Z/` 保存各版本发布文件，已在 .gitignore
- **平台命名**：darwin = macOS, linux = Linux; arm64 = Apple Silicon/ARM, x86_64 = Intel
- **校验和必须**：install.sh 会验证 SHA256，没有 checksums.txt 安装会失败
- **Release Notes**：用英文，包含 What's New 和 Checksums 两部分
