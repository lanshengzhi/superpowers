# Superpowers 仓库维护与上游同步指南

本仓库是一个 Fork 版本，包含自定义修改。为了在不干扰原作者（obra/superpowers）的前提下保持更新，请遵循以下流程。

## 1. 环境配置

当前仓库已配置双远程地址：
- **origin**: 指向您的个人 Fork 仓库 (`git@github.com:lanshengzhi/superpowers.git`)。
- **upstream**: 指向原始仓库 (`https://github.com/obra/superpowers.git`)。

### 安全防护
为了防止意外推送到上游，已执行以下命令禁止对 `upstream` 的 push 操作：
```bash
git remote set-url --push upstream no_push
```

## 2. 日常同步流程 (方案 A：变基)

推荐使用 `rebase` 方式，这会将您的自定义修改始终保持在提交历史的最上方，使历史线保持整洁。

### 快捷命令
在 `main` 分支执行：
```bash
# 1. 获取上游最新代码
git fetch upstream

# 2. 将本地修改变基到上游最新代码之上
git rebase upstream/main

# 3. 强制推送到您的个人远程仓库
git push origin main --force
```

### 处理冲突
如果 `rebase` 过程中出现冲突：
1. 手动解决冲突文件。
2. `git add <文件名>`
3. `git rebase --continue`

## 3. 维护自定义修改的建议

- **提交频率**：建议将您的自定义逻辑（如本项目中的 `MAINTENANCE.md` 或对 Skills 的调整）及时 `git commit`。变基操作会自动识别并重放这些提交。
- **分支建议**：如果修改非常庞大，建议在独立分支工作，同步后再合并回 `main`。
- **测试验证**：同步完成后，建议运行 `tests/` 下的脚本，确保上游的更新没有破坏您的自定义功能。

---
*最后更新时间：2026年4月26日*
