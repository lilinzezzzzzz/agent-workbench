# Commit Message Template

Use this as the default output shape. Keep it compact unless the change genuinely needs more structure.

## Draft Only

Use when the user asked for a message but not for an actual commit.

```text
建议的 commit message:

<type>(<scope>): <subject>
```

If `scope` is unnecessary, omit it:

```text
建议的 commit message:

<type>: <subject>
```

## Draft With Body

Use when the subject alone cannot convey necessary context for the selected change set.
Use bullets for parallel subchanges or independently useful facts. Use concise prose for a connected rationale. Follow the user's requested format and applicable repository convention.

```text
建议的 commit message:

<type>(<scope>): <subject>

- <body bullet 1>
- <body bullet 2>
```

## Draft With Breaking Change

```text
建议的 commit message:

<type>(<scope>): <subject>

BREAKING CHANGE: <what changed for callers>
```

## Commit Executed

Use only after observing successful commit creation and verifying the resulting commit. A request to commit or an attempted command is not evidence of success.

```text
已提交：<commit-sha>

<exact commit message>

<仅在相关时说明剩余改动>
```

If useful, explain an evidence-backed classification choice briefly. Do not report commit-scope uncertainty as an assumption after committing. Resolve material scope ambiguity before execution.

## Blocked Cases

### Nothing staged

For a message-only request, use a user-provided diff or explicit range even when nothing is staged. If no usable change set is available, explain the missing evidence and ask which changes to describe.

For a commit request with nothing staged, report that commit execution is blocked by the staging prerequisite. Keep any prepared message explicitly labeled as a draft.

### Mixed concerns

```text
当前 staged changes 包含多个无关关注点，不建议强行生成单一 commit message。
建议先拆分或重新 stage，再提交。
```

## Example Messages

```text
feat(auth): 添加 JWT 刷新令牌接口
fix(api): 修复分页参数为空时的 500 错误
refactor(vector): 拆分 embedding client 初始化逻辑
perf(db): 减少知识库列表接口的 N+1 查询
test(chunk): 补充分块任务失败重试场景覆盖
chore: 更新开发环境 pre-commit 配置
```
