# skills-for-gpt

约束 LLM 输出风格的 skill 集合。当前包含一对内容完全对齐的中英文 skill，用于让模型的回答**精简、结论先行、可直接使用**。

Skills that constrain LLM output style. Currently contains a pair of fully-aligned English/Chinese skills that make model answers **concise, conclusion-first, and ready to use**.

## 安装 / Install

通过 npm 下载 / Download via npm:

```bash
npm install @mulou/skills-for-gpt
```

安装后把 SKILL.md 复制到你的 agent skills 目录 / After install, copy the SKILL.md files into your agent's skills folder:

```bash
# Claude Code (英文版 / English)
cp -r node_modules/@mulou/skills-for-gpt/concise-response ~/.claude/skills/
# Claude Code (中文版 / Chinese)
cp -r node_modules/@mulou/skills-for-gpt/concise-response-zh ~/.claude/skills/
```

Codex 用户把目标改为 `~/.codex/skills/`。不想装依赖，可用 `npm pack @mulou/skills-for-gpt` 下载 tarball，解压即得两个 SKILL.md。
Codex users: target `~/.codex/skills/` instead. To grab the files without a dependency, run `npm pack @mulou/skills-for-gpt` and unpack the tarball.

## Skills

| Skill | 语言 / Language | 说明 / Description |
|---|---|---|
| [`concise-response`](concise-response/SKILL.md) | English | Concise, conclusion-first answering style |
| [`concise-response-zh`](concise-response-zh/SKILL.md) | 中文 | 精简回答风格（与英文版内容一致） |

## 核心规则 / Core Rules

两个 skill 强制执行同一套规则 / Both skills enforce the same rules:

1. **结论先行** — 第一句话直接给答案，再解释必要原因。
   *Conclusion first — the first sentence is the answer; reasons come after.*
2. **语言简单准确** — 不堆砌术语，术语首次出现时解释。
   *Plain, precise language — no jargon stacking; explain terms on first use.*
3. **简单问题 1～3 句话** — 不加背景、免责声明或"另外"段落。
   *Simple questions get 1–3 sentences — no padding.*
4. **解释用「结论 → 原因 → 怎么做」结构。**
   *Explanations follow Conclusion → Reason → What to do.*
5. **不注水** — 不复述问题、不重复结论、不扩展无关背景。
   *No filler — don't restate the question, repeat the conclusion, or add unrelated background.*
6. **不知道就明说** — 信息不足时说"目前无法确定"，并指出缺什么。
   *Admit uncertainty — say what exactly is missing instead of guessing.*
7. **报告文字可直接使用** — 只给最终正式文本，不加元说明。
   *Report text is paste-ready — final formal wording only.*
8. **给一个答案，不给菜单** — 除非用户要求，不给长列表、大表格或多套方案。
   *One answer, not a menu — no Plan A/B/C unless asked.*
9. **风险警告是精简的例外** — 涉及安全、数据或工程风险时加必要警告，但保持一两句话。
   *Risk warnings are the exception — necessary, but kept to a sentence or two.*

每个 skill 还包含**发送前自检清单**和**反面模式**（禁止出现的典型写法），把风格要求变成可核对的动作。
Each skill also includes a **pre-send checklist** and **anti-patterns** section that turn the style rules into checkable actions.

## 使用方法 / Usage

将 skill 目录放入你的 agent 的 skills 目录（例如 Codex 的 `~/.codex/skills/`，或 Claude Code 的 `.claude/skills/`）。每个 skill 是一个包含 `SKILL.md` 的目录，frontmatter 中的 `description` 描述了触发条件，供 agent 自动匹配加载。

Place a skill directory into your agent's skills folder (e.g. `~/.codex/skills/` for Codex, or `.claude/skills/` for Claude Code). Each skill is a directory containing a `SKILL.md`; the frontmatter `description` states the trigger conditions for automatic loading.

按需选择语言版本：面向中文对话用 `concise-response-zh`，面向英文对话用 `concise-response`，也可以两个都装。

Pick the version matching your conversation language — or install both.
