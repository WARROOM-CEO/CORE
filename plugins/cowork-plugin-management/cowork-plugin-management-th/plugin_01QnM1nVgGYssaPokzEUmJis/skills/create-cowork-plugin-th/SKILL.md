---
name: create-cowork-plugin-th-th
description: >
  แนะนำผู้ใช้ในการสร้างปลั๊กอินใหม่ตั้งแต่ต้นในเซสชัน Cowork
  ใช้เมื่อผู้ใช้ต้องการสร้างปลั๊กอิน, ทำปลั๊กอินใหม่, พัฒนาปลั๊กอิน, สร้างโครงร่างปลั๊กอิน,
  เริ่มปลั๊กอินจากศูนย์, ออกแบบปลั๊กอิน,
  create a plugin, build a plugin, make a new plugin, develop a plugin, scaffold a plugin,
  start a plugin from scratch, design a plugin.
  This skill requires Cowork mode with access to the outputs directory for delivering the final .plugin file.
compatibility: Requires Cowork desktop app environment with access to the outputs directory for delivering .plugin files.
---

# Create Cowork Plugin

Build a new plugin from scratch through guided conversation. Walk the user through discovery, planning, design, implementation, and packaging — delivering a ready-to-install `.plugin` file at the end.

> **Language**: All user-facing output — todo list items, AskUserQuestion labels and options, phase summaries, component plan tables, and any text the user will read — must be written in **Thai (ภาษาไทย)**. Internal logic, file paths, code, schema fields, and technical values remain in English.

## Overview

A plugin is a self-contained directory that extends Claude's capabilities with skills, agents, hooks, and MCP server integrations. This skill encodes the full plugin architecture and a five-phase workflow for creating one conversationally.

The process:

1. **Discovery** — understand what the user wants to build
2. **Component Planning** — determine which component types are needed
3. **Design & Clarifying Questions** — specify each component in detail
4. **Implementation** — create all plugin files
5. **Review & Package** — deliver the `.plugin` file

> **Nontechnical output**: Keep all user-facing conversation in plain Thai. Do not expose implementation details like file paths, directory structures, or schema fields unless the user asks. Frame everything in terms of what the plugin will do.

## Plugin Architecture

### Directory Structure

Every plugin follows this layout:

```
plugin-name/
├── .claude-plugin/
│   └── plugin.json           # Required: plugin manifest
├── skills/                   # Skills (subdirectories with SKILL.md)
│   └── skill-name/
│       ├── SKILL.md
│       └── references/
├── agents/                   # Subagent definitions (.md files)
├── .mcp.json                 # MCP server definitions
└── README.md                 # Plugin documentation
```

> **Legacy `commands/` format**: Older plugins may include a `commands/` directory with single-file `.md` slash commands. This format still works, but new plugins should use `skills/*/SKILL.md` instead — the Cowork UI presents both as a single "Skills" concept, and the skills format supports progressive disclosure via-th `references/`.

**Rules:**

- `.claude-plugin/plugin.json` is always required
- Component directories (`skills/`, `agents/`) go at the plugin root, not inside `.claude-plugin/`
- Only create directories for components the plugin actually uses
- Use kebab-case for all directory and file names

### plugin.json Manifest

Located at `.claude-plugin/plugin.json`. Minimal required field is `name`.

```json
{
  "name": "plugin-name",
  "version": "0.1.0",
  "description": "Brief explanation of plugin purpose",
  "author": {
    "name": "Author Name"
  }
}
```

**Name rules:** kebab-case, lowercase with hyphens, no spaces or special characters.
**Version:** semver format (MAJOR.MINOR.PATCH). Start at `0.1.0`.

Optional fields: `homepage`, `repository`, `license`, `keywords`.

Custom component paths can be specified (supplements, does not replace, auto-discovery):

```json
{
  "commands": "./custom-commands",
  "agents": ["./agents",-th "./specialized-agents"],
  "hooks": "./config/hooks.json",
  "mcpServers": "./.mcp.json"
}
```

### Component Schemas

Detailed schemas for each component type are in `references/component-schemas.md`. Summary:

| Component                          | Location            | Format                      |
| ---------------------------------- | ------------------- | --------------------------- |
| Skills                             | `skills/*/SKILL.md` | Markdown + YAML frontmatter-th |
| MCP Servers                        | `.mcp.json`         | JSON                        |
| Agents (uncommonly used in Cowork) | `agents/*.md`       | Markdown + YAML frontmatter |
| Hooks (rarely used in Cowork)      | `hooks/hooks.json`  | JSON                        |
| Commands (legacy)                  | `commands/*.md`     | Markdown + YAML frontmatter |

This schema is shared with Claude Code's plugin system, but you're creating a plugin for Claude Cowork, a desktop app for doing knowledge work.
Cowork users will usually find skills the most useful. **Scaffold new plugins with `skills/*/SKILL.md` — do not create `commands/` unless the user explicitly needs the legacy single-file-th format.**

### Customizable plugins with `~~` placeholders

> **Do not use or ask about this pattern by default.** Only introduce `~~` placeholders if the user explicitly says they want people outside their organization to use the plugin.

When a plugin is intended to be shared with others outside their company, it might have parts that need to be adapted to individual users.
Use generic language and mark these as requiring customization with two tilde characters such as `create an issue in ~~project tracker`.
If used any tool categories, write a `CONNECTORS.md` file at the plugin root.

### ${CLAUDE_PLUGIN_ROOT} Variable

Use `${CLAUDE_PLUGIN_ROOT}` for all intra-plugin path references in hooks and MCP configs. Never hardcode absolute paths.

## Guided Workflow

When you ask the user something, use AskUserQuestion with Thai labels and options. Don't assume "industry standard" defaults are correct. Note: AskUserQuestion always includes a Skip button and a free-text input box for custom answers, so do not include `None` or `Other` as options.

### Phase 1: Discovery

**Goal**: Understand what the user wants to build and why.

Ask in Thai (only what is unclear — skip questions if the user's initial request already answers them):

- ปลั๊กอินนี้ควรทำอะไร? แก้ปัญหาอะไร?
- ใครจะใช้และในบริบทใด?
- ต้องเชื่อมต่อกับเครื่องมือหรือบริการภายนอกหรือไม่?
- มีปลั๊กอินหรือเวิร์กโฟลว์ที่คล้ายกันเพื่ออ้างอิงหรือไม่?

Summarize your understanding in Thai and confirm before proceeding.

**Output**: Clear statement of plugin purpose and scope (in Thai for the user).

### Phase 2: Component Planning

**Goal**: Determine which component types the plugin needs.

Based on the discovery answers, determine:

- **Skills** — Does it need specialized knowledge that Claude should load on-demand, or user-initiated actions?
- **MCP Servers** — Does it need external service integration?
- **Agents (uncommon)** — Are there autonomous multi-step tasks?
- **Hooks (rare)** — Should something happen automatically on certain events?

Present a component plan table in Thai, including component types you decided not to create:

```
| ส่วนประกอบ | จำนวน | วัตถุประสงค์ |
|-----------|-------|-------------|
| Skill     | 3     | ความรู้เฉพาะด้าน X, ทำสิ่งนี้, ตรวจสอบสิ่งนั้น |
| Agent     | 0     | ไม่จำเป็น |
| Hook      | 1     | ตรวจสอบการเขียน |
| MCP       | 1     | เชื่อมต่อกับบริการ Y |
```

Get user confirmation or adjustments (in Thai) before proceeding.

**Output**: Confirmed list of components to create.

### Phase 3: Design & Clarifying Questions

**Goal**: Specify each component in detail. Resolve all ambiguities before implementation.

For each component type in the plan, ask targeted design questions in Thai. Present questions grouped by component type. Wait for answers before proceeding.

**Skills:**

- คำถามหรือคำสั่งใดของผู้ใช้ควรเรียกใช้ skill นี้?
- ครอบคลุมด้านความรู้ใด?
- ควรมีไฟล์อ้างอิงสำหรับเนื้อหาละเอียด?
- หาก skill เป็นการกระทำที่ผู้ใช้เริ่มต้น: รับ argument อะไร และต้องใช้เครื่องมือใด?

**Agents:**

- ควรทำงานเชิงรุกหรือเฉพาะเมื่อร้องขอ?
- ต้องใช้เครื่องมือใด?
- รูปแบบผลลัพธ์ควรเป็นอย่างไร?

**Hooks:**

- เหตุการณ์ใด? (PreToolUse, PostToolUse, Stop, SessionStart, etc.)
- พฤติกรรมอะไร — ตรวจสอบ บล็อก แก้ไข เพิ่มบริบท?
- แบบ prompt (LLM-driven) หรือแบบ command (deterministic script)?

**MCP Servers:**

- ประเภทเซิร์ฟเวอร์? (stdio สำหรับ local, SSE สำหรับ hosted, HTTP สำหรับ REST API)
- วิธีการยืนยันตัวตน?
- ควรเปิดให้ใช้เครื่องมือใด?

If the user says "whatever you think is best," provide specific recommendations in Thai and get explicit confirmation.

**Output**: Detailed specification for every component.

### Phase 4: Implementation

**Goal**: Create all plugin files following best practices.

**Order of operations:**

1. Create the plugin directory structure
2. Create `plugin.json` manifest
3. Create each component (see `references/component-schemas.md` for exact formats)
4. Create `README.md` documenting the plugin

**Implementation guidelines:**

- **Skills** use progressive disclosure: lean SKILL.md body (under 3,000 words), detailed content in `references/`. Frontmatter description must include specific trigger phrases (Thai phrases if targeting Thai users). Skill bodies are instructions FOR Claude, not messages to the user — write them as directives.
- **Agents** need a description with `<example>` blocks showing triggering conditions, plus a system prompt in the markdown body.
- **Hooks** config goes in `hooks/hooks.json`. Use `${CLAUDE_PLUGIN_ROOT}` for script paths. Prefer prompt-based hooks for complex logic.
- **MCP configs** go in `.mcp.json` at plugin root. Use `${CLAUDE_PLUGIN_ROOT}` for local server paths. Document required env vars in README.

### Phase 5: Review & Package

**Goal**: Deliver the finished plugin.

1. Summarize what was created in Thai — list each component and its purpose
2. Ask in Thai if the user wants any adjustments
3. Run `claude plugin validate <path-to-plugin-json>`; fix any errors and warnings
4. Package as a `.plugin` file:

```bash
cd /path/to/plugin-dir && zip -r /tmp/plugin-name.plugin . -x "*.DS_Store" && cp /tmp/plugin-name.plugin-th /path/to/outputs/plugin-name.plugin
```

> **Important**: Always create the zip in `/tmp/` first, then copy to the outputs folder. Writing directly to the outputs folder may fail due to-th permissions.

> **Naming**: Use the plugin name from `plugin.json` for the `.plugin` file (e.g., if name is `code-reviewer`, output `code-reviewer.plugin`).

The `.plugin` file will appear in the chat as a rich preview where the user can browse the files and accept the plugin by pressing a button.

## Best Practices

- **Start small**: Begin with the minimum viable set of components. A plugin with one well-crafted skill is more useful than one with five half-baked components.
- **Progressive disclosure for skills**: Core knowledge in SKILL.md, detailed reference material in `references/`, working examples in `examples/`.
- **Clear trigger phrases**: Skill descriptions should include specific phrases users would say. Agent descriptions should include `<example>` blocks.
- **Skills are for Claude**: Write skill body content as instructions for Claude to follow, not documentation for the user to read.
- **Imperative writing style**: Use verb-first instructions in skills ("Parse the config file," not "You should parse the config file").
- **Portability**: Always use `${CLAUDE_PLUGIN_ROOT}` for intra-plugin paths, never hardcoded paths.
- **Security**: Use environment variables for credentials, HTTPS for remote servers, least-privilege tool access.

## Additional Resources

- **`references/component-schemas.md`** — Detailed format specifications for every component type (skills, agents, hooks, MCP, legacy commands, CONNECTORS.md)
- **`references/example-plugins.md`** — Three complete example plugin structures at different complexity levels
