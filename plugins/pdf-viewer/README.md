# pdf-viewer

**Plugin ตัวแสดงผล PDF แบบโต้ตอบสำหรับ Cowork — เวอร์ชันภาษาไทย**

Plugin นี้ช่วยให้คุณเปิด อธิบายประกอบ กรอกแบบฟอร์ม และเซ็นชื่อ PDF ในตัวแสดงผลสดที่มี visual feedback แบบ real-time ทำงานได้โดยไม่ต้องเชื่อมต่อบริการภายนอก

---

## ภาพรวมการทำงาน

Plugin ทำงานผ่าน **MCP server ในเครื่อง** (`@modelcontextprotocol/server-pdf`) ที่เริ่มต้นอัตโนมัติเมื่อโหลด plugin ไม่ต้องใช้ API key หรือบัญชีบริการใดๆ

มีสองวิธีใช้งาน:

**Commands (User-invoked)** — workflow เฉพาะที่เรียกด้วย slash command เช่น `/pdf-viewer:open`, `/pdf-viewer:annotate`, `/pdf-viewer:fill-form`, `/pdf-viewer:sign` ใช้สำหรับงานที่มีโครงสร้างชัดเจน

**Skill (Model-invoked)** — `view-pdf` ทำงานอัตโนมัติเมื่อ Claude ตรวจจับว่าคุณต้องการดู ทำเครื่องหมาย หรือร่วมมือบน PDF โดยไม่ต้องพิมพ์ slash command

สิ่งสำคัญ: Plugin นี้เหมาะสำหรับ **workflow แบบโต้ตอบและภาพ** ถ้าคุณต้องการแค่สรุปหรือดึงข้อความ Claude อ่าน PDF โดยตรงได้โดยไม่ต้องใช้ตัวแสดงผล

---

## Skills ทั้งหมด

### `/pdf-viewer:open` — เปิด PDF (User-invoked)

**ใช้เมื่อ:** ต้องการดู PDF ในตัวแสดงผลสด

**สิ่งที่ทำ:** เปิดไฟล์ PDF จาก local path หรือ URL → แสดงในตัวแสดงผล → เสนอขั้นตอนถัดไปตามประเภทเอกสาร (สัญญา, แบบฟอร์ม, บทความวิชาการ)

**Trigger:** `/pdf-viewer:open [path หรือ URL]`

---

### `/pdf-viewer:annotate` — อธิบายประกอบ PDF (User-invoked)

**ใช้เมื่อ:** ต้องการ highlight, เพิ่มหมายเหตุ, ประทับตรา หรือทำเครื่องหมายบนเอกสาร

**สิ่งที่ทำ:** Claude เดินทางผ่านเอกสารทีละส่วน → เสนอชุด annotations → รอการอนุมัติ → ใช้และแสดง screenshot → ให้คุณตรวจสอบและปรับแก้ → ดำเนินการส่วนถัดไป

**Trigger:** `/pdf-viewer:annotate [path หรือ URL]`

---

### `/pdf-viewer:fill-form` — กรอกแบบฟอร์ม PDF (User-invoked)

**ใช้เมื่อ:** ต้องการกรอก PDF ที่มีช่องแบบฟอร์ม

**สิ่งที่ทำ:** ตรวจสอบช่องแบบฟอร์มทั้งหมด → ถ้าชื่อช่องเข้าใจยาก Claude จะ screenshot เพื่อดู label จริง → ถามค่าที่ต้องการและกรอก → แสดง screenshot เพื่อยืนยัน รองรับทั้งแบบ user-driven (กรอกก่อนเปิด) และ AI-assisted (ช่วยกรอกไปด้วยกัน)

**Trigger:** `/pdf-viewer:fill-form [path หรือ URL]`

---

### `/pdf-viewer:sign` — เซ็นชื่อ PDF (User-invoked)

**ใช้เมื่อ:** ต้องการวางลายเซ็นหรืออักษรย่อบนเอกสาร

**สิ่งที่ทำ:** ขอ path รูปลายเซ็น (PNG/JPG) → เปิด PDF → หาตำแหน่งช่องลายเซ็นหรือถามตำแหน่ง → วางรูปลายเซ็น → ยืนยันด้วย screenshot

**Trigger:** `/pdf-viewer:sign [path ของ PDF] [path ของรูปลายเซ็น]`

> **หมายเหตุ:** วางรูปลายเซ็นเท่านั้น — ไม่ใช่ลายเซ็นดิจิทัลที่รับรองทางกฎหมาย

---

### `view-pdf` — ตัวแสดงผล PDF แบบโต้ตอบ (Model-invoked, อัตโนมัติ)

**Trigger:** "แสดง PDF นี้", "เปิดสัญญา", "highlight ส่วนสำคัญ", "ช่วยกรอกแบบฟอร์ม", "เซ็นหน้า 3"

**สิ่งที่ทำ:** ให้ Claude เข้าถึงเครื่องมือ PDF ทั้งหมด — เปิด, อธิบายประกอบ, กรอกแบบฟอร์ม, เซ็นชื่อ, screenshot เพื่อยืนยัน

**ความเชื่อมโยงระหว่าง Skills:** Skill `view-pdf` เป็น engine หลักที่ commands ทุกตัวใช้ร่วมกัน — `/pdf-viewer:open` เปิดเอกสารก่อน จากนั้น `/pdf-viewer:annotate`, `/pdf-viewer:fill-form` และ `/pdf-viewer:sign` ใช้ตัวแสดงผลที่เปิดอยู่แล้วต่อ (ผ่าน `viewUUID`) เพื่อดำเนินการ workflow ต่อไปโดยไม่ต้องเปิด PDF ซ้ำ

---

## โครงสร้างไฟล์ (Bilingual Design)

| ไฟล์/โฟลเดอร์ | ภาษา | ใช้โดย | วัตถุประสงค์ |
|---------------|------|--------|--------------|
| `skills/view-pdf/SKILL.md` | อังกฤษ + Thai directive | Claude | คำสั่งการทำงานหลักของ skill |
| `skills/view-pdf/SKILL-TH.md` | ไทยทั้งหมด | ผู้ใช้ | เปิดอ่านทำความเข้าใจ skill |
| `commands/annotate.md` | อังกฤษ + Thai directive | Claude | คำสั่ง slash command annotate |
| `commands/annotate-TH.md` | ไทยทั้งหมด | ผู้ใช้ | คำแปลคำสั่ง annotate |
| `commands/fill-form.md` | อังกฤษ + Thai directive | Claude | คำสั่ง slash command fill-form |
| `commands/fill-form-TH.md` | ไทยทั้งหมด | ผู้ใช้ | คำแปลคำสั่ง fill-form |
| `commands/open.md` | อังกฤษ + Thai directive | Claude | คำสั่ง slash command open |
| `commands/open-TH.md` | ไทยทั้งหมด | ผู้ใช้ | คำแปลคำสั่ง open |
| `commands/sign.md` | อังกฤษ + Thai directive | Claude | คำสั่ง slash command sign |
| `commands/sign-TH.md` | ไทยทั้งหมด | ผู้ใช้ | คำแปลคำสั่ง sign |
| `CONNECTORS.md` | อังกฤษ | Claude | ข้อมูล MCP server สำหรับ Claude |
| `CONNECTORS-TH.md` | ไทยทั้งหมด | ผู้ใช้ | คำแปลคู่มือการเชื่อมต่อ |
| `.mcp.json` | — | Cowork | กำหนดค่า MCP server อัตโนมัติ |
| `.claude-plugin/plugin.json` | — | Cowork | Metadata ของ plugin |

---

## สัญญาอนุญาต (License)

### งานต้นฉบับ

ปลั๊กอินนี้ดัดแปลงมาจาก **pdf-viewer** โดย Anthropic, PBC ซึ่งเผยแพร่ภายใต้ **Apache License, Version 2.0**

```
Copyright Anthropic, PBC

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0
```

### งานดัดแปลง (Derivative Work)

**pdf-viewer (Localized)** เป็นงานดัดแปลง (Derivative Work) ตามนิยามของ Apache License 2.0 โดย **WARROOM-CEO** มีการเปลี่ยนแปลงดังนี้:

- เพิ่ม Thai Language Instruction Block ใน `SKILL.md` และ `commands/*.md` ทั้ง 4 ไฟล์
- แปล `description` ใน frontmatter ของทุก command และ skill เป็นภาษาไทย
- เพิ่มไฟล์ `SKILL-TH.md` ใน `skills/view-pdf/`: คำแปลภาษาไทยสำหรับผู้ใช้
- เพิ่มไฟล์ `commands/*-TH.md` ทั้ง 4 ไฟล์: คำแปลคำสั่งภาษาไทยสำหรับผู้ใช้
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

*pdf-viewer (Localized) — ดัดแปลงจาก Anthropic pdf-viewer v0.2.0 โดย WARROOM-CEO*
