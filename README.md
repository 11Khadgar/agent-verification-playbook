# Agent Verification Playbook

**"Done" is not "Passed".**

Five `SKILL.md` files that gate an AI coding agent's output *before* anyone is allowed to call it finished. Not a framework, not a plugin — plain markdown procedures an agent loads on demand.

Most agent tooling answers *"can the agent do X?"*. This repo answers *"how do we know it actually did X?"*.

| Skill | Gate it enforces | Turn it on when |
|---|---|---|
| [`handoff-notebook`](skills/handoff-notebook/) | State lives on disk, not in the chat | 3+ steps, multi-file, or spans sessions/days |
| [`deep-fix-gates`](skills/deep-fix-gates/) | A patch you'd hand to a maintainer | Filing an issue, sending a PR, or "my fix was rejected" |
| [`orchestrate-agent-team-delivery`](skills/orchestrate-agent-team-delivery/) | Contracts + file ownership + independent review | A feature that splits into ≥3 independently deliverable modules |
| [`image-quality-workflow`](skills/image-quality-workflow/) | Acceptance criteria for generated assets | Any image generation or edit that ships |
| [`check-native-ecosystem-before-building`](skills/check-native-ecosystem-before-building/) | Look before you build | Platform integration, picking an approach, "why did we miss this option" |

Common thread: **a claim of completion must be backed by a command, a number, or a named unverified item.** Every skill ends with a `Verification` section, and none of them lets you delete or loosen a test to manufacture a pass.

## Install

```bash
git clone https://github.com/11Khadgar/agent-verification-playbook.git
mkdir -p ~/.agents/skills
ln -s "$PWD/agent-verification-playbook/skills/"* ~/.agents/skills/
```

- Pi (≥0.54) discovers `~/.agents/skills` and `.agents/skills` automatically.
- Claude Code and other harnesses that follow the Agent Skills convention: point the symlink at your own skills directory instead.
- No install wanted? Each folder is a single self-contained `SKILL.md`; read it and paste the relevant part into your prompt.

## What this is not

- **Not enforcement.** These are instructions an agent may follow, not interception hooks. Nothing here can stop a model from claiming success.
- **Not portable across harnesses at the mechanics level.** Where a skill needs a concrete mechanism (spawning subagents, structured output, image channels), the harness-specific part is quarantined in an **Appendix** and dated. The principles above it are harness-agnostic.
- **Not version-pinned.** No promise of compatibility with any current or future upstream release. Appendices are snapshots, and they rot.
- **Not a team-in-a-box.** Three of these skills exist mainly to tell you *when not to use them* — don't open a team for a two-file fix, don't use a skill for a one-line change, don't spawn subagents for a single read.

## Repo map

```
skills/          the five procedures
docs/            how-this-system-evolved.md — the essay behind them
examples/        AGENTS.md.example — the rules layer above the skills
.github/         issue template for reporting a rule that failed on your setup
```

---

## 中文

**「完成」不等于「通过」。**

五个 `SKILL.md`，作用是在任何人说「做完了」之前，先把输出卡一道闸。不是框架、不是插件，就是按需加载的纯 markdown 规程。

现在的 agent 工具大多在回答「agent 能不能做 X」；这里回答的是「怎么证明它真的做了 X」。

| Skill | 卡的是什么 | 什么时候用 |
|---|---|---|
| `handoff-notebook` | 状态落盘，不靠对话记忆 | 3 步以上、改多个文件、跨会话或跨天 |
| `deep-fix-gates` | 敢交给维护者的补丁 | 提 issue、提 PR、「我的修复被拒了」 |
| `orchestrate-agent-team-delivery` | 契约 + 文件所有权 + 独立审查 | 能拆成 ≥3 个可独立交付的模块 |
| `image-quality-workflow` | 生成物的验收标准 | 任何要交付的生图或修图 |
| `check-native-ecosystem-before-building` | 动手前先看生态 | 接平台、选方案、「怎么漏了这个」 |

共同点是：**一句「完成」必须有命令、数字或明确的未验证项兜着。** 每个 skill 都以 `Verification` 收尾，且都不允许用删测试、放宽断言的方式制造通过。

### 安装

```bash
git clone https://github.com/11Khadgar/agent-verification-playbook.git
mkdir -p ~/.agents/skills
ln -s "$PWD/agent-verification-playbook/skills/"* ~/.agents/skills/
```

不想装也行：每个目录只有一个 `SKILL.md`，直接读、直接贴进提示词。

### 边界

- **不是强制拦截**：这是 agent 可能遵循的规程，不是 hook。拦不住模型自吹。
- **机械层不跨 harness**：凡涉及具体机制（派子代理、结构化输出、生图通道），都隔离进带日期的**附录**；附录以上的原则与工具无关。
- **不承诺版本兼容**：附录是快照，会过期。
- **不是万能团队模板**：其中三个 skill 的主要作用之一是告诉你**什么时候别用**——两个文件的改动别开团队，一行改动别套 skill，单次读取别派子代理。

## License

MIT. See [LICENSE](LICENSE). Feedback via [Issues](https://github.com/11Khadgar/agent-verification-playbook/issues) — the template asks what failed on *your* setup, which is the only review that matters.
