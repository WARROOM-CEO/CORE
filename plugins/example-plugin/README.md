# example-plugin — Thai Edition

**ปลั๊กอินตัวอย่างอ้างอิงสำหรับนักพัฒนา Claude Code Plugin แสดงโครงสร้างและรูปแบบทุกประเภท พร้อม Localization ภาษาไทย**

---

## ภาพรวมการทำงาน

Plugin นี้ไม่ได้ทำงานเป็น workflow ต่อเนื่อง แต่เป็น **ตัวอย่างอ้างอิง (Reference Template)** ที่แสดงรูปแบบ Plugin ทั้ง 3 ประเภทในไฟล์เดียวกัน:

- **Model-invoked Skill** — Claude เรียกเองตามบริบทของงาน (ตัวอย่าง: `example-skill-th`)
- **User-invoked Skill (Slash Command)** — ผู้ใช้เรียกด้วย `/ชื่อ` (ตัวอย่าง: `example-command-th`)
- **Legacy Command** — รูปแบบเก่าในโฟลเดอร์ `commands/` (ตัวอย่าง: `commands/example-command.md`)

นักพัฒนาสามารถใช้ Plugin นี้เป็นต้นแบบสำหรับสร้าง Plugin ใหม่ โดย copy โครงสร้างและปรับเปลี่ยนตามต้องการ

---

## Skills ทั้งหมด

### 1. `example-skill-th` — Model-invoked

**หน้าที่:** แสดงโครงสร้างและรูปแบบของ Model-invoked Skill — Claude เรียกใช้เองโดยอัตโนมัติเมื่อเห็นว่าเกี่ยวข้องกับงาน ไม่ต้องพิมพ์คำสั่ง

**เรียกใช้เมื่อ:** ผู้ใช้พูดถึง "สร้าง skill", "ดู template ของ skill", "อธิบาย skill", "demonstrate skills", "show skill format", "create a skill template"

**สิ่งที่ Skill นี้สอน:**
- โครงสร้าง frontmatter ของ Model-invoked Skill
- วิธีเขียน description ให้ trigger แม่น รวม trigger phrases ภาษาไทย
- แนวทาง Bilingual Design (SKILL.md + SKILL-TH.md)
- กฎตั้งชื่อ `-th` suffix เพื่อป้องกันชนกับ Official skills

---

### 2. `example-command-th` — User-invoked (Slash Command)

**หน้าที่:** แสดงโครงสร้างและ frontmatter options ของ User-invoked Slash Command

**เรียกใช้ด้วย:**
```
/example-command-th <required-arg> [optional-arg]
```

**สิ่งที่ Skill นี้สอน:**
- frontmatter fields: `argument-hint`, `allowed-tools`, `model`
- ความแตกต่างระหว่าง `skills/<name>/SKILL.md` (รูปแบบใหม่) กับ `commands/*.md` (Legacy)
- วิธีรับ `$ARGUMENTS` จากผู้ใช้มาใช้งานใน Skill

---

### ความเชื่อมโยงระหว่าง Skills

| Skill | ประเภท | ผู้เรียกใช้ | สิ่งที่สอน |
|-------|--------|-----------|-----------|
| `example-skill-th` | Model-invoked | Claude (อัตโนมัติ) | การสร้าง Model-invoked Skill |
| `example-command-th` | User-invoked | ผู้ใช้ (`/example-command-th`) | การสร้าง Slash Command |

ทั้งสอง Skill เป็น **คู่เปรียบเทียบ** ให้เห็นความแตกต่างระหว่างสองรูปแบบหลักของ Claude Code Plugin Skill

---

## โครงสร้างไฟล์ (Bilingual Design)

```
example-plugin/
├── .claude-plugin/
│   └── plugin.json                       # metadata: ชื่อ, author WARROOM-CEO
├── .mcp.json                             # MCP server config (ปัจจุบัน: {} เปล่า)
│                                         # หมายเหตุ: ต้องไม่มี placeholder URL
│                                         # ไม่เช่นนั้น plugin validation จะ fail
├── skills/
│   ├── example-skill/                    # ตัวอย่าง Model-invoked Skill
│   │   ├── SKILL.md                      # คำสั่ง Claude (EN + ไทยส่วนสื่อกับผู้ใช้)
│   │   └── SKILL-TH.md                   # คำแปลไทยสำหรับผู้ใช้อ่าน
│   └── example-command/                  # ตัวอย่าง User-invoked Slash Command (รูปแบบใหม่)
│       ├── SKILL.md                      # คำสั่ง Claude (EN + ไทยส่วนสื่อกับผู้ใช้)
│       └── SKILL-TH.md                   # คำแปลไทยสำหรับผู้ใช้อ่าน
├── commands/
│   └── example-command.md               # ตัวอย่าง Slash Command รูปแบบ Legacy
│                                         # ทำงานเหมือน skills/example-command/SKILL.md ทุกประการ
│                                         # สำหรับ Plugin ใหม่แนะนำให้ใช้ skills/ แทน
├── LICENSE                               # Apache 2.0 ฉบับเต็ม (EN, เอกสารกฎหมาย)
└── README.md                             # เอกสารนี้ (ไทย)
```

| ไฟล์/Folder | ภาษา | ใช้โดย | วัตถุประสงค์ |
|-------------|------|--------|--------------|
| `skills/*/SKILL.md` | EN + ไทย (ส่วนสื่อผู้ใช้) | Claude | คำสั่งหลัก ประหยัด Token |
| `skills/*/SKILL-TH.md` | ไทยทั้งหมด | ผู้ใช้ | อ่านทำความเข้าใจ Skill |
| `commands/*.md` | EN + ไทย (ส่วนสื่อผู้ใช้) | Claude | Legacy slash command format |
| `.mcp.json` | JSON | Claude Code | เชื่อมต่อ MCP server ภายนอก (ถ้ามี) |

---

## สัญญาอนุญาต (License)

### งานต้นฉบับ

ปลั๊กอินนี้ดัดแปลงมาจาก **example-plugin** โดย Anthropic, PBC ซึ่งเผยแพร่ภายใต้ **Apache License, Version 2.0**

```
Copyright Anthropic, PBC

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0
```

### งานดัดแปลง (Derivative Work)

**example-plugin (Thai Edition)** เป็นงานดัดแปลง (Derivative Work) ตามนิยามของ Apache License 2.0 โดย **WARROOM-CEO** มีการเปลี่ยนแปลงดังนี้:

- แก้ไข `skills/example-skill/SKILL.md`: เพิ่ม Thai Language Instruction Block, เปลี่ยนชื่อเป็น `example-skill-th`, เพิ่ม trigger phrases ภาษาไทย
- แก้ไข `skills/example-command/SKILL.md`: เพิ่ม Thai Language Instruction Block, เปลี่ยนชื่อเป็น `example-command-th`
- แก้ไข `commands/example-command.md`: เพิ่ม Thai Language Instruction Block
- เพิ่ม `skills/example-skill/SKILL-TH.md`: คำแปลภาษาไทยเต็มรูปแบบ
- เพิ่ม `skills/example-command/SKILL-TH.md`: คำแปลภาษาไทยเต็มรูปแบบ
- แก้ไข `.mcp.json`: เปลี่ยนจาก placeholder URL `mcp.example.com` เป็น `{}` เพื่อให้ผ่าน plugin validation
- เขียนใหม่ `README.md` เป็นภาษาไทย ตามมาตรฐาน Bilingual Design Pattern
- แก้ไข `plugin.json`: เปลี่ยน author จาก Anthropic เป็น WARROOM-CEO

งานดัดแปลงนี้เผยแพร่ภายใต้ **Apache License, Version 2.0** เช่นเดียวกัน ดูไฟล์ `LICENSE` สำหรับข้อความสัญญาอนุญาตฉบับเต็ม

### สรุปสิทธิ์ตาม Apache 2.0

| สิทธิ์ | รายละเอียด |
|--------|-----------|
| ✅ ใช้งานส่วนตัวและเชิงพาณิชย์ | ใช้ได้อย่างอิสระในทุกบริบท |
| ✅ ดัดแปลงและแจกจ่าย | สามารถแก้ไขและแชร์ต่อได้ |
| ✅ สร้างงานดัดแปลง | นำไปต่อยอดได้ภายใต้ license เดิมหรือที่เข้ากันได้ |

| เงื่อนไข | รายละเอียด |
|----------|-----------|
| 📋 ระบุการเปลี่ยนแปลง | ไฟล์ที่แก้ไขต้องมีหมายเหตุว่าถูกเปลี่ยนแปลง |
| 📋 คงไว้ซึ่งลิขสิทธิ์ต้นฉบับ | ต้องแนบประกาศลิขสิทธิ์ของ Anthropic ไว้ด้วย |
| 📋 แนบไฟล์ LICENSE | ต้องมีไฟล์ `LICENSE` ในทุกการแจกจ่าย |
| ❌ ห้ามใช้เครื่องหมายการค้า | ห้ามนำชื่อ Anthropic ไปใช้ทางการตลาดโดยไม่ได้รับอนุญาต |

---

*example-plugin Thai Edition — ดัดแปลงจาก Anthropic example-plugin โดย WARROOM-CEO*
