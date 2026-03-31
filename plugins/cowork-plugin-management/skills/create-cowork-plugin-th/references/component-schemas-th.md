# Schema ส่วนประกอบ

ข้อกำหนดรูปแบบละเอียดสำหรับส่วนประกอบปลั๊กอินทุกประเภท ใช้อ้างอิงเมื่อสร้างส่วนประกอบในขั้นที่ 4

## Skill

**ตำแหน่ง**: `skills/skill-name/SKILL.md`
**รูปแบบ**: Markdown พร้อม YAML frontmatter

### ฟิลด์ Frontmatter

| ฟิลด์ | จำเป็น | ประเภท | คำอธิบาย |
| --- | --- | --- | --- |
| `name` | ใช่ | String | ตัวระบุ skill (ตัวพิมพ์เล็ก ขีดกลาง; ตรงกับชื่อไดเรกทอรี) |
| `description` | ใช่ | String | คำอธิบายบุรุษที่สามพร้อมวลีทริกเกอร์ |
| `metadata` | ไม่ | Map | คู่ key-value ตามต้องการ (เช่น `version`, `author`) |

### ตัวอย่าง Skill

```yaml
---
name: api-design
description: >
  ควรใช้ skill นี้เมื่อผู้ใช้ขอ "ออกแบบ API",
  "สร้าง API endpoint", "ตรวจสอบโครงสร้าง API", หรือต้องการคำแนะนำ
  เกี่ยวกับแนวปฏิบัติที่ดีสำหรับ REST API, การตั้งชื่อ endpoint, หรือการออกแบบ request/response
metadata:
  version: "0.1.0"
---
```

### กฎการเขียน

- **คำอธิบาย frontmatter**: บุรุษที่สาม ("ควรใช้ skill นี้เมื่อ...") พร้อมวลีทริกเกอร์เฉพาะในเครื่องหมายอัญประกาศ
- **Body**: รูปแบบคำสั่ง ("แยกวิเคราะห์ไฟล์กำหนดค่า" ไม่ใช่ "คุณควรแยกวิเคราะห์ไฟล์กำหนดค่า")
- **ความยาว**: SKILL.md body ไม่เกิน 3,000 คำ (แนะนำ 1,500-2,000) ย้ายเนื้อหาละเอียดไปที่ `references/`

### โครงสร้างไดเรกทอรี Skill

```
skill-name/
├── SKILL.md              # ความรู้หลัก (จำเป็น)
├── references/           # เอกสารละเอียดที่โหลดตามต้องการ
│   ├── patterns.md
│   └── advanced.md
├── examples/             # ตัวอย่างโค้ดที่ใช้งานได้
│   └── sample-config.json
└── scripts/              # สคริปต์ยูทิลิตี้
    └── validate.sh
```

### ระดับ Progressive Disclosure

1. **Metadata** (อยู่ในบริบทเสมอ): ชื่อ + คำอธิบาย (~100 คำ)
2. **SKILL.md body** (เมื่อ skill ถูกเรียกใช้): ความรู้หลัก (<5,000 คำ)
3. **ทรัพยากรที่ bundled มา** (ตามต้องการ): เอกสารอ้างอิง ตัวอย่าง สคริปต์ (ไม่จำกัด)

## Agent

**ตำแหน่ง**: `agents/agent-name.md`
**รูปแบบ**: Markdown พร้อม YAML frontmatter

### ฟิลด์ Frontmatter

| ฟิลด์ | จำเป็น | ประเภท | คำอธิบาย |
| --- | --- | --- | --- |
| `name` | ใช่ | String | ตัวพิมพ์เล็ก ขีดกลาง 3-50 ตัวอักษร |
| `description` | ใช่ | String | เงื่อนไขทริกเกอร์พร้อมบล็อก `<example>` |
| `model` | ใช่ | String | `inherit`, `sonnet`, `opus`, หรือ `haiku` |
| `color` | ใช่ | String | `blue`, `cyan`, `green`, `yellow`, `magenta`, `red` |
| `tools` | ไม่ | Array | จำกัดเครื่องมือเฉพาะ |

### ตัวอย่าง Agent

```markdown
---
name: code-reviewer
description: ใช้ agent นี้เมื่อผู้ใช้ขอตรวจสอบโค้ดอย่างละเอียด หรือต้องการวิเคราะห์คุณภาพโค้ด ความปลอดภัย และแนวปฏิบัติที่ดี

<example>
Context: ผู้ใช้เพิ่งเขียนโมดูลใหม่
user: "ช่วยรีวิวโค้ดนี้ให้หน่อยได้ไหม?"
assistant: "จะใช้ agent code-reviewer เพื่อวิเคราะห์อย่างละเอียด"
<commentary>
ผู้ใช้ขอรีวิวอย่างชัดเจน ซึ่งตรงกับความเชี่ยวชาญของ agent นี้
</commentary>
</example>

<example>
Context: ผู้ใช้กำลังจะ merge PR
user: "ช่วยตรวจก่อน merge ได้ไหม"
assistant: "จะรันการตรวจสอบอย่างครอบคลุมโดยใช้ agent code-reviewer"
<commentary>
การรีวิวก่อน merge ได้ประโยชน์จากกระบวนการวิเคราะห์แบบมีโครงสร้างของ agent
</commentary>
</example>

model: inherit
color: blue
tools: ["Read", "Grep", "Glob"]
---

คุณคือผู้เชี่ยวชาญด้านการตรวจสอบโค้ดที่มุ่งเน้นการระบุปัญหาด้านความปลอดภัย ประสิทธิภาพ การบำรุงรักษา และความถูกต้อง

**หน้าที่หลัก:**

1. วิเคราะห์โครงสร้างและการจัดระเบียบโค้ด
2. ระบุช่องโหว่ด้านความปลอดภัย
3. ชี้จุดที่มีปัญหาด้านประสิทธิภาพ
4. ตรวจสอบการปฏิบัติตามแนวปฏิบัติที่ดี

**กระบวนการวิเคราะห์:**

1. อ่านไฟล์ทั้งหมดในขอบเขต
2. ระบุรูปแบบและรูปแบบที่ไม่ดี
3. จัดหมวดหมู่ผลการค้นพบตามความรุนแรง
4. เสนอข้อเสนอแนะการแก้ไขเฉพาะ

**รูปแบบผลลัพธ์:**
นำเสนอผลการค้นพบแบ่งตามความรุนแรง (วิกฤต, คำเตือน, ข้อมูล) พร้อม:

- path ไฟล์และหมายเลขบรรทัด
- คำอธิบายปัญหา
- ข้อเสนอแนะการแก้ไข
```

### กฎการตั้งชื่อ Agent

- 3-50 ตัวอักษร
- ตัวพิมพ์เล็ก ตัวเลข ขีดกลาง เท่านั้น
- ต้องเริ่มต้นและลงท้ายด้วยตัวอักษรหรือตัวเลข
- ห้ามใช้ขีดล่าง ช่องว่าง หรืออักขระพิเศษ

### แนวทางการเลือกสี

- น้ำเงิน/ฟ้า: วิเคราะห์ ตรวจสอบ
- เขียว: งานที่เน้นความสำเร็จ
- เหลือง: ข้อควรระวัง การตรวจสอบ
- แดง: วิกฤต ความปลอดภัย
- ม่วง: ความคิดสร้างสรรค์ การสร้าง

## Hook

**ตำแหน่ง**: `hooks/hooks.json`
**รูปแบบ**: JSON

### เหตุการณ์ที่ใช้ได้

| เหตุการณ์ | เมื่อใดที่ทำงาน |
| --- | --- |
| `PreToolUse` | ก่อนการเรียกใช้เครื่องมือ |
| `PostToolUse` | หลังการเรียกใช้เครื่องมือเสร็จ |
| `Stop` | เมื่อ Claude ตอบเสร็จ |
| `SubagentStop` | เมื่อ subagent ทำงานเสร็จ |
| `SessionStart` | เมื่อเซสชันเริ่มต้น |
| `SessionEnd` | เมื่อเซสชันสิ้นสุด |
| `UserPromptSubmit` | เมื่อผู้ใช้ส่งข้อความ |
| `PreCompact` | ก่อนการบีบอัดบริบท |
| `Notification` | เมื่อมีการแจ้งเตือน |

### ประเภท Hook

**แบบ prompt** (แนะนำสำหรับ logic ซับซ้อน):

```json
{
  "type": "prompt",
  "prompt": "ประเมินว่าการเขียนไฟล์นี้เป็นไปตามแบบแผนของโปรเจกต์หรือไม่: $TOOL_INPUT",
  "timeout": 30
}
```

เหตุการณ์ที่รองรับ: Stop, SubagentStop, UserPromptSubmit, PreToolUse

**แบบ command** (การตรวจสอบแบบแน่นอน):

```json
{
  "type": "command",
  "command": "bash ${CLAUDE_PLUGIN_ROOT}/hooks/scripts/validate.sh",
  "timeout": 60
}
```

### ตัวอย่าง hooks.json

```json
{
  "PreToolUse": [
    {
      "matcher": "Write|Edit",
      "hooks": [
        {
          "type": "prompt",
          "prompt": "ตรวจสอบว่าการเขียนไฟล์นี้เป็นไปตามมาตรฐานการเขียนโค้ดของโปรเจกต์ หากละเมิดมาตรฐาน ให้อธิบายเหตุผลและบล็อก",
          "timeout": 30
        }
      ]
    }
  ],
  "SessionStart": [
    {
      "matcher": "",
      "hooks": [
        {
          "type": "command",
          "command": "cat ${CLAUDE_PLUGIN_ROOT}/context/project-context.md",
          "timeout": 10
        }
      ]
    }
  ]
}
```

### รูปแบบผลลัพธ์ Hook (Command Hook)

Command hook คืนค่า JSON ไปที่ stdout:

```json
{
  "decision": "block",
  "reason": "การเขียนไฟล์ละเมิดแบบแผนการตั้งชื่อ"
}
```

ค่าที่เป็นไปได้: `approve` (อนุมัติ), `block` (บล็อก), `ask_user` (ขอยืนยันจากผู้ใช้)

## MCP เซิร์ฟเวอร์

**ตำแหน่ง**: `.mcp.json` ที่ root ปลั๊กอิน
**รูปแบบ**: JSON

### ประเภทเซิร์ฟเวอร์

**stdio** (กระบวนการ local):

```json
{
  "mcpServers": {
    "my-server": {
      "command": "node",
      "args": ["${CLAUDE_PLUGIN_ROOT}/servers/server.js"],
      "env": {
        "API_KEY": "${API_KEY}"
      }
    }
  }
}
```

**SSE** (เซิร์ฟเวอร์ระยะไกล, transport แบบ server-sent events):

```json
{
  "mcpServers": {
    "asana": {
      "type": "sse",
      "url": "https://mcp.asana.com/sse"
    }
  }
}
```

**HTTP** (เซิร์ฟเวอร์ระยะไกล, transport แบบ streamable HTTP):

```json
{
  "mcpServers": {
    "api-service": {
      "type": "http",
      "url": "https://api.example.com/mcp",
      "headers": {
        "Authorization": "Bearer ${API_TOKEN}"
      }
    }
  }
}
```

### การแทนที่ Environment Variable

กำหนดค่า MCP ทั้งหมดรองรับการแทนที่ `${VAR_NAME}`:

- `${CLAUDE_PLUGIN_ROOT}` — ไดเรกทอรีปลั๊กอิน (ใช้เสมอเพื่อ portability)
- `${ANY_ENV_VAR}` — environment variable ของผู้ใช้

บันทึก environment variable ที่จำเป็นทั้งหมดใน README ของปลั๊กอิน

### รายการไดเรกทอรีที่ไม่มี URL

รายการไดเรกทอรี MCP บางรายการไม่มี `url` เนื่องจาก endpoint เป็นแบบ dynamic ปลั๊กอินสามารถอ้างอิงเซิร์ฟเวอร์เหล่านี้โดย **ชื่อ** แทน — หากชื่อ MCP เซิร์ฟเวอร์ในกำหนดค่าปลั๊กอินตรงกับชื่อรายการไดเรกทอรี จะถือว่าเหมือนกับการจับคู่ URL

## Command (แบบเดิม)

> **แนะนำใช้ `skills/*/SKILL.md` สำหรับปลั๊กอินใหม่** UI ของ Cowork แสดง command และ skill เป็นหมวด "Skills" เดียวกัน รูปแบบ `commands/` ยังใช้ได้ แต่ใช้เฉพาะเมื่อต้องการรูปแบบไฟล์เดียวที่มีการแทนที่ `$ARGUMENTS`/`$1` และการรัน bash แบบ inline

**ตำแหน่ง**: `commands/command-name.md`
**รูปแบบ**: Markdown พร้อม YAML frontmatter เสริม

### ฟิลด์ Frontmatter

| ฟิลด์ | จำเป็น | ประเภท | คำอธิบาย |
| --- | --- | --- | --- |
| `description` | ไม่ | String | คำอธิบายสั้นที่แสดงใน `/help` (ไม่เกิน 60 ตัวอักษร) |
| `allowed-tools` | ไม่ | String หรือ Array | เครื่องมือที่ command ใช้ได้ |
| `model` | ไม่ | String | ตั้งค่าโมเดล: `sonnet`, `opus`, `haiku` |
| `argument-hint` | ไม่ | String | บันทึก argument ที่คาดหวังสำหรับ autocomplete |

### ตัวอย่าง Command

```markdown
---
description: ตรวจสอบโค้ดเรื่องความปลอดภัย
allowed-tools: Read, Grep, Bash(git:*)
argument-hint: [file-path]
---

ตรวจสอบ @$1 เพื่อหาช่องโหว่ด้านความปลอดภัย ได้แก่:

- SQL injection
- การโจมตี XSS
- การหลีกเลี่ยงการยืนยันตัวตน
- การจัดการข้อมูลที่ไม่ปลอดภัย

ระบุหมายเลขบรรทัดเฉพาะ ระดับความรุนแรง และข้อเสนอแนะการแก้ไข
```

### กฎสำคัญ

- Command เป็นคำสั่งสำหรับ Claude ไม่ใช่ข้อความสำหรับผู้ใช้ เขียนเป็นคำสั่ง
- `$ARGUMENTS` จับ argument ทั้งหมดเป็น string เดียว; `$1`, `$2`, `$3` จับ argument ตามตำแหน่ง
- syntax `@path` รวมเนื้อหาไฟล์ในบริบทของ command
- syntax `!` backtick รัน bash แบบ inline เพื่อบริบทแบบ dynamic (เช่น `` !`git diff --name-only` ``)
- ใช้ `${CLAUDE_PLUGIN_ROOT}` เพื่ออ้างอิงไฟล์ปลั๊กอินอย่างพกพาได้

### รูปแบบ allowed-tools

```yaml
# เครื่องมือเฉพาะ
allowed-tools: Read, Write, Edit, Bash(git:*)

# Bash เฉพาะคำสั่งที่กำหนด
allowed-tools: Bash(npm:*), Read

# เครื่องมือ MCP (เฉพาะ)
allowed-tools: ["mcp__plugin_name_server__tool_name"]
```

## CONNECTORS.md

**ตำแหน่ง**: root ปลั๊กอิน
**เมื่อต้องสร้าง**: เมื่อปลั๊กอินอ้างอิงเครื่องมือภายนอกตามหมวดหมู่แทนผลิตภัณฑ์เฉพาะ

### รูปแบบ

```markdown
# Connectors

## การอ้างอิงเครื่องมือทำงานอย่างไร

ไฟล์ปลั๊กอินใช้ `~~หมวดหมู่` เป็น placeholder สำหรับเครื่องมือที่ผู้ใช้
เชื่อมต่อในหมวดหมู่นั้น ตัวอย่างเช่น `~~เครื่องมือจัดการโปรเจกต์` อาจหมายถึง
Asana, Linear, Jira หรือเครื่องมือจัดการโปรเจกต์อื่นๆ ที่มี MCP เซิร์ฟเวอร์

ปลั๊กอินเป็นแบบ tool-agnostic — อธิบายเวิร์กโฟลว์ในแง่ของหมวดหมู่
แทนผลิตภัณฑ์เฉพาะ

## Connectors สำหรับปลั๊กอินนี้

| หมวดหมู่ | Placeholder | เซิร์ฟเวอร์ที่รวมมา | ตัวเลือกอื่น |
| --- | --- | --- | --- |
| แชท | `~~แชท` | Slack | Microsoft Teams, Discord |
| เครื่องมือจัดการโปรเจกต์ | `~~เครื่องมือจัดการโปรเจกต์` | Linear | Asana, Jira, Monday |
```

### การใช้ Placeholder ~~

ในไฟล์ปลั๊กอิน (skill, agent) อ้างอิงเครื่องมือแบบทั่วไป:

```markdown
ตรวจสอบ ~~เครื่องมือจัดการโปรเจกต์ สำหรับ ticket ที่เปิดอยู่ที่มอบหมายให้ผู้ใช้
โพสต์สรุปไปที่ ~~แชท ในช่องทีม
```

ระหว่างการปรับแต่ง (ผ่าน skill cowork-plugin-customizer) placeholder เหล่านี้จะถูกแทนที่ด้วยชื่อเครื่องมือเฉพาะ

## README.md

ปลั๊กอินทุกตัวควรมี README ที่ประกอบด้วย:

1. **ภาพรวม** — ปลั๊กอินทำอะไร
2. **ส่วนประกอบ** — รายการ skill, agent, hook, MCP เซิร์ฟเวอร์
3. **การตั้งค่า** — environment variable หรือการกำหนดค่าที่จำเป็น
4. **การใช้งาน** — วิธีเรียกใช้แต่ละ skill
5. **การปรับแต่ง** — ถ้ามี CONNECTORS.md ให้กล่าวถึง
