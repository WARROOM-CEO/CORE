# sales

**Plugin Sales Productivity สำหรับ Cowork — เวอร์ชันภาษาไทย**

Plugin นี้ช่วยให้ทีม sales ค้นหา prospect, สร้าง outreach, จัดการ pipeline และวางกลยุทธ์ดีลได้เร็วขึ้น ทำงานได้แบบ standalone ด้วย web search หรือเชื่อมต่อ CRM, อีเมล และเครื่องมืออื่นๆ เพื่อประสิทธิภาพสูงสุด

---

## ภาพรวมการทำงาน

Plugin ทำงานสองโหมด:

**Commands (User-invoked)** — workflows เฉพาะที่เรียกด้วย slash command เช่น `/call-summary`, `/forecast`, `/pipeline-review` ใช้สำหรับงานที่มีโครงสร้างชัดเจนและต้องการ output ที่เป็นระบบ

**Skills (Model-invoked)** — ความรู้ domain ที่ Claude โหลดอัตโนมัติเมื่อ request เกี่ยวข้อง เช่น เมื่อพูดว่า "research Acme Corp" Claude จะ trigger `account-research` โดยอัตโนมัติ ไม่ต้องพิมพ์ slash command

ทุก command และ skill ทำงานได้แบบ **Standalone** (paste notes, upload CSV หรืออธิบายสถานการณ์) และดีขึ้นมากเมื่อ **เชื่อมต่อ MCP** (CRM, อีเมล, transcripts)

---

## Skills ทั้งหมด

### `/call-summary` — สรุป Call (User-invoked)

**ใช้เมื่อ:** หลัง call ทุกประเภท ต้องการ action items, follow-up email และสรุปภายใน

**สิ่งที่ทำ:** ประมวลผล notes หรือ transcript → ดึง action items พร้อมเจ้าของ → ร่าง follow-up email → สร้างสรุปภายในทีม → เสนอ log ใน CRM (ถ้าเชื่อมต่อ)

---

### `/forecast` — พยากรณ์ยอดขาย (User-invoked)

**ใช้เมื่อ:** เตรียม quarterly forecast, ประเมิน gap-to-quota, ตัดสินใจ commit vs. upside

**สิ่งที่ทำ:** รับ pipeline CSV หรือคำอธิบาย → สร้าง weighted forecast พร้อม best/likely/worst → แยก commit vs. upside → gap analysis เทียบ quota

---

### `/pipeline-review` — ทบทวน Pipeline (User-invoked)

**ใช้เมื่อ:** weekly pipeline review, โฟกัสดีลสำคัญ, ตรวจจับปัญหา

**สิ่งที่ทำ:** วิเคราะห์ pipeline health → จัดลำดับดีล → แจ้ง risk flags (stale, past close date, single-threaded) → แผนงานรายสัปดาห์

---

### `account-research` — วิจัย Account (Model-invoked, อัตโนมัติ)

**Trigger:** "research [company]", "ค้นหาข้อมูล [person]", "intel on [prospect]"

**สิ่งที่ทำ:** ภาพรวมบริษัท, ผู้ติดต่อสำคัญ, ข่าวล่าสุด, สัญญาณการจ้างงาน, แนวทาง outreach ที่แนะนำ

---

### `call-prep` — เตรียมตัวก่อน Call (Model-invoked, อัตโนมัติ)

**Trigger:** "เตรียมตัว call กับ [company]", "prep me for [meeting]"

**สิ่งที่ทำ:** บริบท account, ข้อมูลผู้เข้าร่วม, agenda ที่แนะนำ, คำถาม discovery, objections ที่อาจเกิดขึ้น

---

### `daily-briefing` — สรุปประจำวัน (Model-invoked, อัตโนมัติ)

**Trigger:** "สรุปประจำเช้า", "daily brief", "วันนี้มีอะไรบ้าง"

**สิ่งที่ทำ:** การประชุมวันนี้, pipeline alerts, อีเมลที่รอตอบ, actions ที่แนะนำ เรียงตามความสำคัญ

---

### `draft-outreach` — ร่าง Outreach (Model-invoked, อัตโนมัติ)

**Trigger:** "ร่าง outreach ถึง [person/company]", "เขียน cold email ถึง [prospect]"

**สิ่งที่ทำ:** วิจัย prospect ก่อน → ระบุ angle ที่ resonates → ร่างอีเมลหลายเวอร์ชัน + LinkedIn message + subject lines

---

### `competitive-intelligence` — วิจัยคู่แข่ง (Model-invoked, อัตโนมัติ)

**Trigger:** "เราต่างจาก [competitor] อย่างไร", "battlecard สำหรับ [competitor]"

**สิ่งที่ทำ:** วิจัยคู่แข่ง → สร้าง interactive battlecard (HTML) → comparison matrix → sales talk tracks

---

### `create-an-asset` — สร้าง Sales Asset (Model-invoked, อัตโนมัติ)

**Trigger:** "สร้าง asset สำหรับ [company]", "ทำ landing page สำหรับ [prospect]"

**สิ่งที่ทำ:** วิจัย prospect → ถาม 3-4 คำถาม → สร้าง asset แบบ branded (landing page, deck, one-pager, workflow demo) เป็นไฟล์ HTML พร้อมแชร์

**ความเชื่อมโยงระหว่าง Skills:** `account-research` มักถูกเรียกก่อนเพื่อรวบรวมข้อมูล prospect → ใช้ใน `call-prep`, `draft-outreach` และ `create-an-asset` / Commands ทั้งสามทำงานร่วมกับ skills: `/call-summary` → อาจ trigger `account-research` เพิ่มเติม, `/forecast` และ `/pipeline-review` → ทำงานเป็น standalone workflow

---

## โครงสร้างไฟล์ (Bilingual Design)

| ไฟล์/โฟลเดอร์ | ภาษา | ใช้โดย | วัตถุประสงค์ |
|---------------|------|--------|--------------|
| `skills/*/SKILL.md` | อังกฤษ + Thai directive | Claude | คำสั่งการทำงานหลัก (ลด token) |
| `skills/*/SKILL-TH.md` | ไทยทั้งหมด | ผู้ใช้ | เปิดอ่านทำความเข้าใจแต่ละ skill |
| `skills/create-an-asset/QUICKREF.md` | อังกฤษ | Claude | Quick reference ภายใน |
| `skills/create-an-asset/QUICKREF-TH.md` | ไทยทั้งหมด | ผู้ใช้ | Cheat sheet ภาษาไทย |
| `skills/create-an-asset/README.md` | อังกฤษ | Claude | รายละเอียดเต็มภายใน |
| `skills/create-an-asset/README-TH.md` | ไทยทั้งหมด | ผู้ใช้ | รายละเอียดเต็มภาษาไทย |
| `CONNECTORS.md` | อังกฤษ | Claude | ข้อมูล MCP connector สำหรับ Claude |
| `CONNECTORS-TH.md` | ไทยทั้งหมด | ผู้ใช้ | คำแปลคู่มือการเชื่อมต่อ |
| `.mcp.json` | — | Cowork | กำหนดค่า MCP server ล่วงหน้า |
| `.claude-plugin/plugin.json` | — | Cowork | Metadata ของ plugin |

---

## สัญญาอนุญาต (License)

### งานต้นฉบับ

ปลั๊กอินนี้ดัดแปลงมาจาก **sales** โดย Anthropic, PBC ซึ่งเผยแพร่ภายใต้ **Apache License, Version 2.0**

```
Copyright Anthropic, PBC

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0
```

### งานดัดแปลง (Derivative Work)

**sales (Localized)** เป็นงานดัดแปลง (Derivative Work) ตามนิยามของ Apache License 2.0 โดย **WARROOM-CEO** มีการเปลี่ยนแปลงดังนี้:

- เพิ่ม Thai Language Instruction Block ใน `SKILL.md` ทั้ง 8 ไฟล์ (รวม create-an-asset)
- แปล `description` ใน frontmatter ของทุก `SKILL.md` เป็นภาษาไทย
- เพิ่มไฟล์ `SKILL-TH.md` ทั้ง 9 ไฟล์ (รวม create-an-asset): คำแปลภาษาไทยสำหรับผู้ใช้
- เพิ่มไฟล์ `QUICKREF-TH.md` และ `README-TH.md` ใน `create-an-asset/`: คำแปลเอกสารประกอบ
- เพิ่มไฟล์ `CONNECTORS-TH.md`: คำแปลคู่มือการเชื่อมต่อเครื่องมือ
- แปล `description` ใน `plugin.json` เป็นภาษาไทย
- เขียน `README.md` ใหม่เป็นภาษาไทยตามรูปแบบมาตรฐาน

งานดัดแปลงนี้เผยแพร่ภายใต้ **Apache License, Version 2.0** เช่นเดียวกัน ดูไฟล์ `LICENSE` สำหรับข้อความสัญญาอนุญาตฉบับเต็ม

### สรุปสิทธิ์ตาม Apache 2.0

| สิทธิ์ | รายละเอียด |
|--------|-----------|
| ✅ ใช้งานส่วนตัวและเชิงพาณิชย์ | ใช้ได้อย่างอิสระในทุกบริบท |
| ✅ ดัดแปลงและแจกจ่าย | สามารถแก้ไขและแชร์ต่อได้ |
| ✅ สร้างงานดัดแปลง | นำไปต่อยอดได้ภายใต้ license เดิมหรือที่เข้ากันได้ |
| ✅ ใช้สิทธิบัตร | ได้รับสิทธิ์ใช้สิทธิบัตรจาก contributor โดยปริยาย |

| เงื่อนไข | รายละเอียด |
|----------|-----------|
| 📋 ระบุการเปลี่ยนแปลง | ไฟล์ที่แก้ไขต้องมีหมายเหตุว่าถูกเปลี่ยนแปลง |
| 📋 คงไว้ซึ่งลิขสิทธิ์ต้นฉบับ | ต้องแนบประกาศลิขสิทธิ์ของ Anthropic ไว้ด้วย |
| 📋 แนบไฟล์ LICENSE | ต้องมีไฟล์ `LICENSE` ในทุกการแจกจ่าย |
| ❌ ห้ามใช้เครื่องหมายการค้า | ห้ามนำชื่อ Anthropic ไปใช้ทางการตลาดโดยไม่ได้รับอนุญาต |

---

*sales (Localized) — ดัดแปลงจาก Anthropic sales v1.2.0 โดย WARROOM-CEO*
