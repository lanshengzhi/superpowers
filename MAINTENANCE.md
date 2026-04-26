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
将 `main` 的最新更改合并到您的开发分支：
```bash
git checkout custom
git merge main
# 或者使用 rebase 以保持历史线性
# git rebase main
```

## 3. 开发建议

- **始终在 custom 分支工作**：不要在 `main` 分支进行任何提交。
- **定期合入上游**：建议每周或在上游有重大更新时执行一次同步。
- **解决冲突**：在 `git merge main` 过程中如果出现冲突，解决后提交即可。

---
*最后更新时间：2026年4月26日*
