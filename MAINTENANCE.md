# Superpowers 仓库维护与上游同步指南 (分支隔离版)

本仓库采用分支隔离策略：
- **main**: 严格作为原始仓库 (`upstream/main`) 的镜像，不包含任何自定义修改。
- **custom**: 存放所有自定义功能、文档和配置。

## 1. 环境配置

- **origin**: 您的个人 Fork (`git@github.com:lanshengzhi/superpowers.git`)。
- **upstream**: 原始仓库 (`https://github.com/obra/superpowers.git`)。

已禁止向 `upstream` 进行任何 push 操作。

## 2. 日常同步流程

### 步骤 A：同步主镜像 (main)
```bash
git checkout main
git fetch upstream
git reset --hard upstream/main
git push origin main --force
```

### 步骤 B：同步自定义分支 (custom)
为了保持提交历史的线性（linear history），必须使用 rebase 而非 merge 将 `main` 的更新合入 `custom`：
```bash
git checkout custom
git rebase main
# 如果发生冲突，解决后运行:
# git add <冲突文件> && git rebase --continue
git push origin custom --force
```

## 3. 开发建议

- **始终在 custom 分支工作**：不要在 `main` 分支进行任何提交。
- **强制线性历史**：禁止在 `custom` 分支使用 `merge` 合并 `main`，始终使用 `rebase`。
- **强制推送**：由于 `rebase` 会改变提交基准，同步后需要使用 `git push origin custom --force`。

---
*最后更新时间：2026年4月26日*
