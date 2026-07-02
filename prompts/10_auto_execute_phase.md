# 自动执行当前 Phase 提示词

请使用 `$ai-coding-workflow` 的「自动执行当前 Phase」命令。

请读取：

- `docs/PRD.md`
- `docs/SPEC.md`
- `docs/TASKS.md`
- `docs/PROGRESS.md`，如果存在

要求：

1. 默认只执行当前 Phase。
2. 当前 Phase 内优先执行 P0。
3. 不执行后续版本任务。
4. 不执行未定义功能。
5. 每个 Task 完成后自测并更新 `docs/PROGRESS.md`。
6. 当前 Phase 完成后停止，输出阶段总结，不自动进入下一个 Phase。
