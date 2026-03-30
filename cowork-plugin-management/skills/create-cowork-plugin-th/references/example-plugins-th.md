# ตัวอย่างปลั๊กอิน

โครงสร้างปลั๊กอินตัวอย่างสมบูรณ์สามระดับความซับซ้อน ใช้เป็นแม่แบบเมื่อสร้างในขั้นที่ 4

## ปลั๊กอินขั้นต่ำ: Skill เดียว

ปลั๊กอินง่ายๆ ที่มี skill เดียวและไม่มีส่วนประกอบอื่น

### โครงสร้าง

```
meeting-notes/
├── .claude-plugin/
│   └── plugin.json
├── skills/
│   └── meeting-notes/
│       └── SKILL.md
└── README.md
```

### plugin.json

```json
{
  "name": "meeting-notes",
  "version": "0.1.0",
  "description": "สร้างบันทึกการประชุมแบบมีโครงสร้างจากการถอดเสียง",
  "author": {
    "name": "ผู้ใช้"
  }
}
```

### skills/meeting-notes/SKILL.md

```markdown
---
name: meeting-notes
description: >
  สร้างบันทึกการประชุมแบบมีโครงสร้างจากการถอดเสียง ใช้เมื่อผู้ใช้ขอ
  "สรุปการประชุม", "สร้างบันทึกการประชุม", "แยก action item จากการถอดเสียง",
  หรือให้ไฟล์ถอดเสียงการประชุม
---

อ่านไฟล์ถอดเสียงที่ผู้ใช้ให้มาและสร้างบันทึกการประชุมแบบมีโครงสร้าง

รวมส่วนเหล่านี้:

1. **ผู้เข้าร่วม** — ระบุรายชื่อผู้เข้าร่วมทั้งหมดที่กล่าวถึง
2. **สรุป** — ภาพรวมของการประชุม 2-3 ประโยค
3. **การตัดสินใจสำคัญ** — รายการตัวเลขของการตัดสินใจที่ทำ
4. **Action Item** — ตารางที่มีคอลัมน์: ผู้รับผิดชอบ, งาน, กำหนดเวลา
5. **คำถามที่ยังไม่ได้ตอบ** — สิ่งที่ยังไม่แก้ไข

เขียนบันทึกลงไฟล์ใหม่ที่ตั้งชื่อตามการถอดเสียงโดยเพิ่ม `-notes` ต่อท้าย
```

---

## ปลั๊กอินมาตรฐาน: Skill + MCP

ปลั๊กอินที่รวมความรู้เฉพาะด้าน การกระทำที่ผู้ใช้เริ่มต้น และการเชื่อมต่อบริการภายนอก

### โครงสร้าง

```
code-quality/
├── .claude-plugin/
│   └── plugin.json
├── skills/
│   ├── coding-standards/
│   │   ├── SKILL.md
│   │   └── references/
│   │       └── style-rules.md
│   ├── review-changes/
│   │   └── SKILL.md
│   └── fix-lint/
│       └── SKILL.md
├── .mcp.json
└── README.md
```

### plugin.json

```json
{
  "name": "code-quality",
  "version": "0.1.0",
  "description": "บังคับใช้มาตรฐานการเขียนโค้ดด้วยการตรวจสอบ linting และคู่มือสไตล์",
  "author": {
    "name": "ผู้ใช้"
  }
}
```

### skills/review-changes/SKILL.md

```markdown
---
name: review-changes
description: >
  ตรวจสอบการเปลี่ยนแปลงโค้ดเรื่องสไตล์และคุณภาพ ใช้เมื่อผู้ใช้ขอ
  "ตรวจสอบการเปลี่ยนแปลง", "เช็ค diff นี้", "ตรวจสอบการละเมิดสไตล์",
  หรือต้องการตรวจสอบคุณภาพโค้ดที่ยังไม่ได้ commit
---

รัน `git diff --name-only` เพื่อรับรายชื่อไฟล์ที่เปลี่ยนแปลง

สำหรับแต่ละไฟล์ที่เปลี่ยนแปลง:

1. อ่านไฟล์
2. ตรวจสอบเทียบกับ skill coding-standards เรื่องการละเมิดสไตล์
3. ระบุ bug หรือรูปแบบที่ไม่ดีที่อาจเกิดขึ้น
4. ชี้จุดที่มีข้อกังวลด้านความปลอดภัย

นำเสนอสรุปพร้อม:

- path ไฟล์
- ระดับความรุนแรง (ข้อผิดพลาด, คำเตือน, ข้อมูล)
- คำอธิบายและข้อเสนอแนะการแก้ไข
```

### skills/fix-lint/SKILL.md

```markdown
---
name: fix-lint
description: >
  แก้ไขปัญหา linting อัตโนมัติในไฟล์ที่เปลี่ยนแปลง ใช้เมื่อผู้ใช้ขอ
  "แก้ไข lint error", "ทำความสะอาด linting", หรือ "แก้ไข lint อัตโนมัติ"
---

รัน linter: `npm run lint -- --format json 2>&1`

แยกวิเคราะห์ผลลัพธ์ linter และแก้ไขแต่ละปัญหา:

- สำหรับปัญหาที่แก้ไขอัตโนมัติได้ ให้ใช้การแก้ไขโดยตรง
- สำหรับปัญหาที่ต้องแก้ไขเอง ให้แก้ไขตามแบบแผนของโปรเจกต์
- ข้ามปัญหาที่ต้องเปลี่ยนแปลงสถาปัตยกรรม

หลังจากแก้ไขทั้งหมด รัน linter อีกครั้งเพื่อยืนยันผลลัพธ์สะอาด
```

### skills/coding-standards/SKILL.md

```yaml
---
name: coding-standards
description: >
  ควรใช้ skill นี้เมื่อผู้ใช้ถามเกี่ยวกับ "มาตรฐานการเขียนโค้ด",
  "คู่มือสไตล์", "แบบแผนการตั้งชื่อ", "กฎการจัดรูปแบบโค้ด", หรือต้องการ
  คำแนะนำเกี่ยวกับความคาดหวังด้านคุณภาพโค้ดเฉพาะโปรเจกต์
metadata:
  version: "0.1.0"
---
```

```markdown
# มาตรฐานการเขียนโค้ด

มาตรฐานและแบบแผนการเขียนโค้ดของโปรเจกต์สำหรับโค้ดที่สม่ำเสมอและมีคุณภาพ

## กฎหลัก

- ใช้ camelCase สำหรับตัวแปรและฟังก์ชัน
- ใช้ PascalCase สำหรับคลาสและ type
- แนะนำ const มากกว่า let; หลีกเลี่ยง var
- ความยาวบรรทัดสูงสุด: 100 ตัวอักษร
- ใช้ return type ที่ชัดเจนบนฟังก์ชันที่ export ทั้งหมด

## ลำดับการ Import

1. แพ็กเกจภายนอก
2. แพ็กเกจภายใน (alias ด้วย @/)
3. import แบบ relative
4. import เฉพาะ type ไว้ท้าย

## แหล่งข้อมูลเพิ่มเติม

- **`references/style-rules.md`** — กฎสไตล์ครบถ้วนแยกตามภาษา
```

### .mcp.json

```json
{
  "mcpServers": {
    "github": {
      "type": "http",
      "url": "https://api.githubcopilot.com/mcp/"
    }
  }
}
```

---

## ปลั๊กอินครบฟีเจอร์: ส่วนประกอบทุกประเภท

ปลั๊กอินที่ใช้ skill, agent, hook และการเชื่อมต่อ MCP พร้อม connector แบบ tool-agnostic

### โครงสร้าง

```
engineering-workflow/
├── .claude-plugin/
│   └── plugin.json
├── skills/
│   ├── team-processes/
│   │   ├── SKILL.md
│   │   └── references/
│   │       └── workflow-guide.md
│   ├── standup-prep/
│   │   └── SKILL.md
│   └── create-ticket/
│       └── SKILL.md
├── agents/
│   └── ticket-analyzer.md
├── hooks/
│   └── hooks.json
├── .mcp.json
├── CONNECTORS.md
└── README.md
```

### plugin.json

```json
{
  "name": "engineering-workflow",
  "version": "0.1.0",
  "description": "ปรับปรุงเวิร์กโฟลว์วิศวกรรม: เตรียม standup จัดการ ticket และคุณภาพโค้ด",
  "author": {
    "name": "ผู้ใช้"
  },
  "keywords": ["engineering", "workflow", "tickets", "standup"]
}
```

### agents/ticket-analyzer.md

```markdown
---
name: ticket-analyzer
description: ใช้ agent นี้เมื่อผู้ใช้ต้องการวิเคราะห์ ticket, คัดกรอง issue ที่เข้ามา, หรือจัดลำดับความสำคัญ backlog

<example>
Context: ผู้ใช้กำลังเตรียมวางแผนสปรินต์
user: "ช่วยคัดกรอง ticket ใหม่เหล่านี้หน่อย"
assistant: "จะใช้ agent ticket-analyzer เพื่อตรวจสอบและจัดหมวดหมู่ ticket"
<commentary>
การคัดกรอง ticket ต้องใช้การวิเคราะห์อย่างเป็นระบบหลายมิติ ทำให้ agent เหมาะสม
</commentary>
</example>

<example>
Context: ผู้ใช้มี backlog จำนวนมาก
user: "จัดลำดับความสำคัญ backlog สำหรับสปรินต์หน้าหน่อย"
assistant: "จะวิเคราะห์ backlog โดยใช้ agent ticket-analyzer เพื่อแนะนำลำดับความสำคัญ"
<commentary>
การจัดลำดับความสำคัญ backlog เป็นงานอัตโนมัติหลายขั้นตอนที่เหมาะกับ agent
</commentary>
</example>

model: inherit
color: cyan
tools: ["Read", "Grep"]
---

คุณคือผู้เชี่ยวชาญด้านการวิเคราะห์ ticket วิเคราะห์ ticket เรื่องลำดับความสำคัญ ขนาดงาน และ dependency

**หน้าที่หลัก:**

1. จัดหมวดหมู่ ticket ตามประเภท (bug, ฟีเจอร์, tech debt, การปรับปรุง)
2. ประมาณขนาดงานเปรียบเทียบ (S, M, L, XL)
3. ระบุ dependency ระหว่าง ticket
4. แนะนำลำดับความสำคัญ

**กระบวนการวิเคราะห์:**

1. อ่านคำอธิบาย ticket ทั้งหมด
2. จัดหมวดหมู่แต่ละรายการตามประเภท
3. ประมาณขนาดงานตามขอบเขต
4. แมป dependency
5. จัดอันดับตามอัตราส่วนผลกระทบต่อขนาดงาน

**รูปแบบผลลัพธ์:**
| Ticket | ประเภท | ขนาดงาน | Dependency | ลำดับความสำคัญ |
|--------|------|--------|-------------|----------|
| ... | ... | ... | ... | ... |

ตามด้วยเหตุผลสั้นๆ สำหรับ 5 อันดับแรก
```

### hooks/hooks.json

```json
{
  "SessionStart": [
    {
      "matcher": "",
      "hooks": [
        {
          "type": "command",
          "command": "echo '## บริบททีม\n\nรอบสปรินต์: 2 สัปดาห์ Standup: ทุกวัน 9:30 น. ใช้ ~~เครื่องมือจัดการโปรเจกต์ สำหรับจัดการ ticket'",
          "timeout": 5
        }
      ]
    }
  ]
}
```

### CONNECTORS.md

```markdown
# Connectors

## การอ้างอิงเครื่องมือทำงานอย่างไร

ไฟล์ปลั๊กอินใช้ `~~หมวดหมู่` เป็น placeholder สำหรับเครื่องมือที่ผู้ใช้
เชื่อมต่อในหมวดหมู่นั้น ปลั๊กอินเป็นแบบ tool-agnostic

## Connectors สำหรับปลั๊กอินนี้

| หมวดหมู่ | Placeholder | เซิร์ฟเวอร์ที่รวมมา | ตัวเลือกอื่น |
| --- | --- | --- | --- |
| เครื่องมือจัดการโปรเจกต์ | `~~เครื่องมือจัดการโปรเจกต์` | Linear | Asana, Jira, Monday |
| แชท | `~~แชท` | Slack | Microsoft Teams |
| Source control | `~~source control` | GitHub | GitLab, Bitbucket |
```

### .mcp.json

```json
{
  "mcpServers": {
    "linear": {
      "type": "sse",
      "url": "https://mcp.linear.app/sse"
    },
    "github": {
      "type": "http",
      "url": "https://api.githubcopilot.com/mcp/"
    },
    "slack": {
      "type": "http",
      "url": "https://slack.mcp.claude.com/mcp"
    }
  }
}
```
