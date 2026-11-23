# SECourseDesign GitHub 协作规范

项目的代码、文档和配置变更通过 Git 提交和 GitHub Pull Request（PR）留痕。

## 1. 分支与日常开发

- `main` 保存可演示、可提交的稳定版本。仅在阶段验收、答辩等发布节点，通过 PR 将 `dev` 合入 `main`。
- `dev` 用于日常集成。任务分支从 `dev` 创建，完成后通过 PR 合回 `dev`。
- `main` 和 `dev` 启用分支保护，所有变更通过 PR 合并，禁止直接推送。仓库初始化时，由仓库负责人从 `main` 创建 `dev`，并为两个分支配置保护。

每个任务使用独立分支，命名格式为 `类型/学号或姓名缩写-简短说明`。

| 分支前缀 | 用途 | 示例 |
| --- | --- | --- |
| `feature/` | 功能开发 | `feature/2450287-login-page` |
| `fix/` | 缺陷修复 | `fix/2450287-order-query-bug` |
| `doc/` | 文档变更 | `doc/2450287-user-guide` |
| `test/` | 测试变更 | `test/2450287-inventory-tests` |

远程 `dev` 建立后，从最新的 `origin/dev` 创建任务分支。

```bash
git fetch origin
git switch -c feature/2450287-login-page origin/dev
```

继续开发已有任务时，先在任务分支同步 `dev`。提交 PR 前再同步一次，解决冲突并验证相关改动后，再推送任务分支。

```bash
git fetch origin
git merge origin/dev
git push -u origin feature/2450287-login-page
```

## 2. Commit 提交

推荐采用 `type(scope): 简短说明` 格式。`scope` 用模块或功能名，说明写清改动。例如 `feat(user): 新增登录表单`、`docs(readme): 补充启动说明`。

| 类型 | 用途 |
| --- | --- |
| `feat` | 新功能 |
| `fix` | 修复问题 |
| `docs` | 文档 |
| `test` | 测试 |
| `refactor` | 重构 |
| `style` | 格式调整，保持逻辑行为一致 |
| `chore` | 工程配置、依赖或杂项维护 |
| `build` | 构建相关变更 |
| `revert` | 回滚提交 |

每次提交聚焦一个明确改动。提交前检查暂存区，排除 `.vs/`、`bin/`、`obj/`、个人截图、临时文件和含真实凭据的本地配置。

## 3. Pull Request 与合并

一个 PR 聚焦一个问题。日常 PR 的目标分支为 `dev`，阶段发布 PR 的目标分支为 `main`。标题推荐使用 `[类型] 简短说明`，例如 `[Feature] 完成供应商查询页面` 或 `[Docs] 补充项目启动说明`。

发起 PR 前检查分支是否存在冲突，并按改动范围完成本地构建、基本运行和相关测试。在 PR 中记录实际检查结果，注明未运行的项目和原因。审查时核对修改范围和验证结果，处理审查意见后再合并。

可在 GitHub PR 描述中使用以下模板。

```markdown
## 本次修改

- 修改内容和影响范围
- 关联 Issue（如有）

## 修改类型

- [ ] 新功能
- [ ] 缺陷修复
- [ ] 文档变更
- [ ] 测试变更
- [ ] 重构或工程配置

## 验证结果

- 执行的命令、测试或手动检查及结果
```
