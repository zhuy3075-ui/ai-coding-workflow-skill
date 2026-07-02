# AI Coding Workflow Skill

这个 Skill 把《AI 编程项目标准作业手册 v2.0》整理成 Codex 可复用 SOP，用于从甲方沟通、PRD、SPEC、TASKS、Phase 执行、验收到最终交付的完整软件项目流程。

## 解决什么问题

- 防止 AI 一上来直接写代码。
- 防止 MVP 范围失控。
- 防止 PRD、SPEC、TASKS、PROGRESS 不一致。
- 防止跨 Phase 连续执行导致验收缺失。
- 防止编造测试结果或跳过 P0 问题。

## 适合什么项目

- 从 0 到 1 的软件 MVP。
- 需要甲方需求澄清和交付验收的项目。
- 已有代码但缺少 PRD / SPEC / TASKS 的项目。
- 需要 Codex 逐 Phase 执行并留下验证证据的项目。

## 不适合什么项目

- 一次性很小的代码修补。
- 没有明确产品目标的探索性闲聊。
- 需要 L3 无人值守、生产权限、付款、凭据或高风险运维的项目，除非用户单独授权并提供风险边界。

## 如何开始使用

1. 把 `SKILL.md` 放入 Codex 可发现的 skills 目录，例如 `~/.codex/skills/ai-coding-workflow/SKILL.md`。
2. 新建项目时先使用 `prompts/01_client_interview.md` 或直接说“使用 ai-coding-workflow 做需求访谈”。
3. 按顺序生成 `docs/PRD.md`、`docs/SPEC.md`、`docs/TASKS.md`。
4. TASKS 审查通过后，再使用“自动执行当前 Phase”。
5. 每个 Phase 完成后必须运行“阶段验收”。

## 每个阶段怎么触发

- 需求访谈: `prompts/01_client_interview.md`
- 生成 PRD: `prompts/02_generate_prd.md`
- 审查 PRD: `prompts/03_review_prd.md`
- 优化 PRD: `prompts/04_optimize_prd.md`
- 生成 SPEC: `prompts/05_generate_spec.md`
- 补充 UI SPEC: `prompts/06_ui_spec.md`
- 审查 SPEC / 优化 SPEC / 最终一致性检查: `prompts/07_review_spec.md`
- 生成 TASKS / 审查 TASKS / 优化 TASKS: `prompts/08_generate_tasks.md`、`prompts/09_review_tasks.md`
- 自动执行当前 Phase: `prompts/10_auto_execute_phase.md`
- 阶段验收: `prompts/11_phase_acceptance.md`
- 修复问题: `prompts/12_debug_fix.md`
- MVP 总验收: `prompts/13_mvp_acceptance.md`
- 交付文档和最终交付验收: `prompts/14_final_delivery.md`

## 如何判断是否可以进入下一阶段

- PRD 进入 SPEC: PRD v2.0 已通过一致性检查，无 P0。
- SPEC 进入 TASKS: SPEC v2.0 与 PRD/UI 一致，无 P0 或必要 P1。
- TASKS 进入开发: TASKS v2.0 审查通过，任务可执行、可验收、依赖清楚。
- Phase 进入下一阶段: 当前 Phase 验收通过，无 P0，必要 P1 已处理或明确不阻塞。
- 进入 MVP 总验收: 所有 P0 和影响 MVP 的必要 P1 完成，`docs/TASKS.md` 与 `docs/PROGRESS.md` 一致。

## 出问题时如何修复

使用 `prompts/12_debug_fix.md`。修复原则:

- 不开发新功能。
- 不执行新 Task。
- 只修当前问题直接相关内容。
- 先修 P0，再修必要 P1。
- 修复后运行回归检查并更新 `docs/PROGRESS.md`。

## 如何交付

1. 运行 MVP 总验收。
2. 生成 `README.md`、`docs/USER_GUIDE.md`、`docs/DELIVERY.md`、`docs/CHANGELOG.md`。
3. 运行最终交付验收。
4. 只有构建、测试、核心流程、文档一致性和已知问题记录都通过时，才输出“可以交付”。
