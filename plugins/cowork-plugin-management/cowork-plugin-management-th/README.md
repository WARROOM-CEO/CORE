# cowork-plugin-management-th

**ปลั๊กอินสำหรับสร้างและปรับแต่ง Claude Code Plugin ภายใน Cowork mode โดย Claude สื่อสารเป็นภาษาไทยตลอดการใช้งาน**

---

## ภาพรวมการทำงาน

Plugin นี้ทำหน้าที่เป็น **"ผู้ช่วยสร้างและปรับแต่ง Plugin"** ครอบคลุมสองกรณีหลัก:

- **สร้างใหม่ตั้งแต่ต้น** — Claude สัมภาษณ์ความต้องการ, ออกแบบโครงสร้าง, เขียนไฟล์ทั้งหมด และแพ็กเกจเป็น `.plugin` พร้อมติดตั้ง
- **ปรับแต่ง Plugin ที่มีอยู่** — Claude ค้นหา placeholder ใน template, รวบรวมข้อมูลองค์กรจาก Slack/Docs/Email อัตโนมัติ แก้ไขค่าจริง และค้นหา MCP server ที่เหมาะสมเพิ่มเติม

ทั้งสอง Skill ต้องใช้ภายใน **Cowork desktop app** เท่านั้น เพราะต้องเข้าถึงไฟล์ Plugin ที่ mount บนเครื่อง

---

## Skills ทั้งหมด

### 1. `cowork-plugin-customizer-th` — Model-invoked

**หน้าที่:** ปรับแต่ง Plugin ที่มีอยู่แล้ว ไม่ว่าจะเป็นการตั้งค่า template ครั้งแรก หรือแก้ไขส่วนเฉพาะเจาะจง

**เรียกใช้เมื่อ:** ผู้ใช้พูดถึง "ปรับแต่งปลั๊กอิน", "ตั้งค่าปลั๊กอิน", "customize plugin", "set up plugin", "configure plugin", "แก้ไข skill ใน plugin"

**กระบวนการทำงาน:**
```
ระบุ Plugin → ตรวจ ~~ placeholders → Phase 0: รวบรวมบริบทจากผู้ใช้
→ Phase 1: ค้นข้อมูลจาก Slack/Docs/Email → Phase 2: สร้าง todo list
→ Phase 3: แก้ไขไฟล์ทีละรายการ → Phase 4: ค้นหาและเชื่อมต่อ MCP
→ แพ็กเกจ .plugin → สรุปผลเป็นภาษาไทย
```

แยกแยะ 3 โหมดอัตโนมัติจากสถานะของ Plugin:
- **Generic setup** — มี `~~placeholder` → แทนด้วยค่าจริงขององค์กร
- **Scoped** — ผู้ใช้ระบุส่วนที่ต้องการเปลี่ยน → แก้เฉพาะจุดนั้น
- **General** — ไม่มี placeholder, ต้องการเปลี่ยนภาพรวม → อ่านทั้งหมดแล้วถาม

---

### 2. `create-cowork-plugin-th` — Model-invoked

**หน้าที่:** สร้าง Plugin ใหม่ตั้งแต่ต้นผ่านกระบวนการสัมภาษณ์และออกแบบ

**เรียกใช้เมื่อ:** ผู้ใช้พูดถึง "สร้างปลั๊กอิน", "ทำปลั๊กอินใหม่", "create a plugin", "build a plugin", "scaffold a plugin", "ออกแบบ plugin"

**กระบวนการทำงาน:**
```
Discovery: ทำความเข้าใจความต้องการ
→ Component Planning: กำหนด Skills, Agents, MCP ที่ต้องการ
→ Design: ระบุรายละเอียดแต่ละส่วน
→ Build: สร้างไฟล์ทั้งหมด (SKILL.md, plugin.json, .mcp.json ฯลฯ)
→ Delivery: แพ็กเกจ .plugin พร้อมส่งให้ผู้ใช้ติดตั้ง
```

---

### ความเชื่อมโยงระหว่าง Skills

| สถานการณ์ | Skill ที่ใช้ | ผลลัพธ์ |
|-----------|------------|---------|
| ยังไม่มี Plugin, ต้องการสร้างใหม่ | `create-cowork-plugin-th` | `.plugin` file ใหม่ |
| มี Plugin แล้ว ต้องการปรับแต่ง | `cowork-plugin-customizer-th` | `.plugin` file ที่ปรับแล้ว |

ทั้งสอง Skill เป็น **คู่แฝด** ที่ทำงานต่อเนื่องกันได้ — สร้างด้วย `create` แล้วปรับในภายหลังด้วย `customizer`

---

## โครงสร้างไฟล์ (Bilingual Design)

```
cowork-plugin-management-th/
├── .claude-plugin/
│   └── plugin.json                           # metadata: ชื่อ, author WARROOM-CEO
├── skills/
│   ├── cowork-plugin-customizer-th/
│   │   ├── SKILL.md                          # คำสั่ง Claude (EN + ไทยส่วนสื่อกับผู้ใช้)
│   │   ├── SKILL-TH.md                       # คำแปลไทยสำหรับผู้ใช้อ่าน
│   │   ├── references/
│   │   │   ├── mcp-servers.md                # รายการ MCP server ทั้งหมดที่รองรับ (EN)
│   │   │   ├── mcp-servers-th.md             # คำแปลภาษาไทย
│   │   │   ├── search-strategies.md          # วิธีค้นหาข้อมูลจาก Slack/Docs/Email (EN)
│   │   │   └── search-strategies-th.md       # คำแปลภาษาไทย
│   │   └── examples/
│   │       └── customized-mcp.json           # ตัวอย่าง .mcp.json ที่ configure แล้ว
│   └── create-cowork-plugin-th/
│       ├── SKILL.md                          # คำสั่ง Claude (EN + ไทยส่วนสื่อกับผู้ใช้)
│       ├── SKILL-TH.md                       # คำแปลไทยสำหรับผู้ใช้อ่าน
│       └── references/
│           ├── component-schemas.md          # JSON schemas สำหรับส่วนประกอบต่างๆ (EN)
│           ├── component-schemas-th.md       # คำแปลภาษาไทย
│           ├── example-plugins.md            # ตัวอย่าง Plugin จริงสำหรับอ้างอิง (EN)
│           └── example-plugins-th.md        # คำแปลภาษาไทย
├── LICENSE                                   # Apache 2.0 ฉบับเต็ม (EN, เอกสารกฎหมาย)
└── README.md                                 # เอกสารนี้ (ไทย)
```

| ไฟล์/Folder | ภาษา | ใช้โดย | วัตถุประสงค์ |
|-------------|------|--------|--------------|
| `skills/*/SKILL.md` | EN + ไทย (ส่วนสื่อผู้ใช้) | Claude | คำสั่งหลัก ประหยัด Token |
| `skills/*/SKILL-TH.md` | ไทยทั้งหมด | ผู้ใช้ | อ่านทำความเข้าใจ Skill |
| `references/*.md` | อังกฤษ | Claude | โหลดเมื่อต้องการ ไม่โหลดทุกครั้ง |
| `references/*-th.md` | ไทยทั้งหมด | ผู้ใช้ | คำแปลเอกสารอ้างอิง |
| `examples/*.json` | — | Claude + ผู้ใช้ | ตัวอย่าง config จริง |

---

## สัญญาอนุญาต (License)

### งานต้นฉบับ

ปลั๊กอินนี้ดัดแปลงมาจาก **cowork-plugin-management** โดย Anthropic, PBC ซึ่งเผยแพร่ภายใต้ **Apache License, Version 2.0**

```
Copyright Anthropic, PBC

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0
```

### งานดัดแปลง (Derivative Work)

**cowork-plugin-management-th** เป็นงานดัดแปลง (Derivative Work) ตามนิยามของ Apache License 2.0 โดย **WARROOM-CEO** มีการเปลี่ยนแปลงดังนี้:

- แก้ไข SKILL.md ทุกไฟล์: เพิ่ม Thai Language Instruction Block, trigger phrases ภาษาไทย, suffix `-th` ให้ชื่อ Skill
- เพิ่ม SKILL-TH.md ทุก Skill: คำแปลภาษาไทยเต็มรูปแบบสำหรับผู้ใช้อ่าน
- เพิ่ม references/*-th.md ทุกไฟล์: คำแปลภาษาไทยของเอกสารอ้างอิงทั้งหมด
- เขียนใหม่ README.md เป็นภาษาไทย ตามมาตรฐาน Bilingual Design Pattern
- แก้ไข plugin.json: เปลี่ยน author จาก Anthropic เป็น WARROOM-CEO

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

*cowork-plugin-management-th v0.2.2 — ดัดแปลงจาก Anthropic cowork-plugin-management โดย WARROOM-CEO*
