# Example Command — ฉบับภาษาไทย

เอกสารนี้เป็นคำแปลภาษาไทยสำหรับผู้ใช้ที่ต้องการเข้าใจโครงสร้างและแนวทางการสร้าง Slash Command สำหรับ Claude Code Plugin

---

## ภาพรวม

Command (หรือ Slash Command) คือ Skill ที่ **ผู้ใช้เรียกใช้เอง** โดยพิมพ์ `/ชื่อ-command` ในช่องสนทนา ต่างจาก Model-invoked Skill ที่ Claude เรียกเองตามบริบท

---

## รูปแบบการเรียกใช้

```
/example-command-th my-argument
/example-command-th arg1 arg2
```

---

## Frontmatter Options

Command รองรับ field เหล่านี้ใน frontmatter:

| Field | จำเป็น | รายละเอียด |
|-------|--------|-----------|
| `name` | ✅ | ตัวระบุ — ใช้เป็นชื่อ slash command (เช่น `name: example-command-th` → `/example-command-th`) |
| `description` | ✅ | คำอธิบายสั้นๆ ที่แสดงใน `/help` |
| `argument-hint` | ❌ | คำแนะนำสำหรับ argument เช่น `<required-arg> [optional-arg]` |
| `allowed-tools` | ❌ | Tools ที่อนุมัติล่วงหน้า ช่วยลด permission prompts เช่น `[Read, Glob, Grep, Bash]` |
| `model` | ❌ | Override model ที่ใช้ เช่น `"haiku"`, `"sonnet"`, `"opus"` |

---

## โครงสร้างไฟล์

### รูปแบบใหม่ (แนะนำ)

```
skills/
└── example-command-th/
    ├── SKILL.md          # ไฟล์หลัก (ภาษาอังกฤษ + ไทยสำหรับส่วนสื่อกับผู้ใช้)
    └── SKILL-TH.md       # คำแปลภาษาไทยสำหรับผู้ใช้อ่าน
```

### รูปแบบเก่า (Legacy)

```
commands/
└── example-command.md    # รูปแบบเก่า — ยังใช้งานได้ แต่ไม่แนะนำสำหรับ Plugin ใหม่
```

> **หมายเหตุ:** ทั้งสองรูปแบบทำงานเหมือนกันทุกประการ ต่างกันแค่โครงสร้างไฟล์เท่านั้น

---

## แนวปฏิบัติที่ดี

- เพิ่ม suffix `-th` ต่อท้ายชื่อ Command เพื่อหลีกเลี่ยงการชนกับ Official skill
- ระบุ `argument-hint` เสมอเพื่อให้ผู้ใช้รู้ว่าต้องส่ง argument อะไร
- ใช้ `allowed-tools` เพื่อลดจำนวนครั้งที่ระบบถาม permission
- เขียน description ทั้งภาษาไทยและอังกฤษเพื่อให้ทำงานได้กับทั้งสองภาษา
- สำหรับ Plugin ใหม่ ให้ใช้รูปแบบ `skills/<name>/SKILL.md` แทน `commands/*.md`
