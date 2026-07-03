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

1. 把本仓库部署到本地 agent 可发现的 skills 目录。
2. 新开一次本地 agent 会话，让 agent 重新读取 skills。
3. 不需要记复杂命令，直接用自然语言说你要做什么。
4. 按顺序生成 `docs/PRD.md`、`docs/SPEC.md`、`docs/TASKS.md`。
5. TASKS 审查通过后，再让 agent “自动执行当前 Phase”。
6. 每个 Phase 完成后必须运行“阶段验收”。

## 本地部署

如果你使用的是本地 Codex 或兼容 skills 的本地 agent，需要做两件事：先安装 skill，再让本地 agent 的 `AGENTS.md` 包含触发规则。

第一步，把仓库克隆到本机 skills 目录：

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/zhuy3075-ui/ai-coding-workflow-skill.git ~/.codex/skills/ai-coding-workflow
```

如果已经安装过，更新时进入目录拉取即可：

```bash
cd ~/.codex/skills/ai-coding-workflow
git pull
```

第二步，把 agentmd 模板应用到本地 agent 实际读取的 `AGENTS.md`。

如果你希望所有本地 Codex 会话都能触发这个 skill，可以先备份再替换全局 agentmd：

```bash
cp ~/.codex/AGENTS.md ~/.codex/AGENTS.md.bak
cp ~/.codex/skills/ai-coding-workflow/agents/AGENTS.ai-coding-workflow.generated.md ~/.codex/AGENTS.md
```

如果你只想让某个项目使用它，就不要替换全局文件，而是把 `agents/AGENTS.ai-coding-workflow.generated.md` 复制到目标项目的 `AGENTS.md`，或把其中 `## 12. Skill 使用策略` 里的 `ai-coding-workflow` 触发规则合并进项目现有的 `AGENTS.md`。

部署后，重新打开本地 agent 会话，或让本地 agent 重新加载 skills。只要本地 agent 能发现 `~/.codex/skills/ai-coding-workflow/SKILL.md`，且当前生效的 `AGENTS.md` 包含 `ai-coding-workflow` 触发规则，就可以用自然语言触发。

## 自然语言怎么触发

用户不需要输入精确命令，也不需要复制 prompt 文件。只要用自然语言描述当前阶段，本地 agent 就应该触发对应流程。例如：

- “帮我先和甲方做需求访谈，确认这个项目的 MVP 范围。”
- “根据这些访谈记录生成 PRD。”
- “审查一下 `docs/PRD.md`，看能不能进入 SPEC。”
- “基于当前 PRD 生成 SPEC，不要扩大 MVP。”
- “检查 PRD、SPEC 和 UI 规格是否一致。”
- “把 PRD 和 SPEC 拆成 TASKS。”
- “执行当前 Phase 的 P0 任务，完成后停止。”
- “对刚才完成的 Phase 做阶段验收。”
- “根据这个报错进入问题修复模式，不要开发新功能。”
- “判断下一步应该继续哪个 Phase，还是进入 MVP 总验收。”
- “做 MVP 总验收，并准备交付文档。”

如果本地 agent 没有自动触发，可以显式加一句：“使用 `ai-coding-workflow` 处理这个任务”。例如：“使用 `ai-coding-workflow`，根据访谈记录生成 PRD。”

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
