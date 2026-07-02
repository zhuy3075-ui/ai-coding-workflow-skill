# 问题定位与修复提示词

请使用 `$ai-coding-workflow` 的「修复问题」命令。

请读取：

- `docs/PRD.md`
- `docs/SPEC.md`
- `docs/TASKS.md`
- `docs/PROGRESS.md`
- 最近一次验收报告、错误报告或测试失败信息

错误信息如下：

【粘贴报错、测试失败日志、截图描述或验收报告问题】

要求：

1. 不开发新功能。
2. 不执行新 Task。
3. 只修复当前问题直接相关内容。
4. 先修 P0，再修必要 P1。
5. 修复后运行回归检查并更新 `docs/PROGRESS.md`。
