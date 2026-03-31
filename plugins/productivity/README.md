# productivity

**Plugin จัดการงานและ Memory สำหรับ Cowork — เวอร์ชันภาษาไทย**

Plugin นี้ให้ Claude ทำงานเหมือนเพื่อนร่วมงานที่รู้จักองค์กรของคุณ — จัดการ task list, สร้าง memory จากบุคคลและโปรเจกต์ที่ทำงานด้วย, และแสดงภาพรวมผ่าน dashboard ที่อัปเดตแบบ real-time

---

## ภาพรวมการทำงาน

Plugin ทำงาน 3 ส่วนหลักร่วมกัน:

**Task Management** — ไฟล์ `TASKS.md` เป็นศูนย์กลางของงานทั้งหมด Claude อ่าน เขียน และอัปเดตไฟล์นี้ตามคำสั่งของคุณ และยังดึง task จาก project tracker ภายนอกมาซิงค์ได้โดยอัตโนมัติ

**Workplace Memory** — ระบบ memory สองชั้น (CLAUDE.md + memory/) สอนให้ Claude เข้าใจ shorthand, ชื่อเล่น, acronym และศัพท์เฉพาะขององค์กร เพื่อให้ตอบสนองคำขอได้เหมือนเพื่อนร่วมงาน ไม่ใช่ chatbot

**Visual Dashboard** — ไฟล์ HTML ในเครื่องที่แสดง board view ของงานและ memory ทั้งหมด แก้ไขจาก board หรือจากไฟล์ก็ sync กันเอง

---

## Skills ทั้งหมด

### `/productivity:start` — เริ่มต้นระบบ (User-invoked)

**ใช้เมื่อ:** ตั้งค่า plugin ครั้งแรก, bootstrap memory จาก task list ที่มีอยู่

**สิ่งที่ทำ:**
- ตรวจสอบและสร้างไฟล์ที่ขาดหายไป (TASKS.md, CLAUDE.md, memory/, dashboard.html)
- Bootstrap memory โดยถอดรหัส shorthand จาก task list ของคุณทีละรายการ
- เสนอสแกน email/calendar/chat เพื่อสร้าง memory ที่ครบถ้วนยิ่งขึ้น

**ความเชื่อมโยงกับ Skills อื่น:** `/start` เป็นจุดเริ่มต้น — ต้องรันก่อน `/update` จึงจะทำงานได้เต็มที่

---

### `/productivity:update` — ซิงค์และรีเฟรช (User-invoked)

**ใช้เมื่อ:** ต้องการซิงค์งานจาก external tools, คัด stale tasks, เติมช่องว่างใน memory

**สองโหมด:**
- `/productivity:update` — ซิงค์ task จาก project tracker, คัด stale tasks, เติม memory gaps
- `/productivity:update --comprehensive` — สแกนลึกทุกแหล่ง (แชท, อีเมล, ปฏิทิน, เอกสาร) เพื่อจับ todos ที่อาจพลาดและเสนอ memory ใหม่

---

### `memory-management` — จัดการ Memory (Model-invoked, อัตโนมัติ)

**ไม่ต้องเรียกใช้เอง** — Claude โหลด skill นี้อัตโนมัติเมื่อต้องถอดรหัส shorthand หรือจัดการ memory

**สิ่งที่ทำ:**
- ถอดรหัส shorthand, ชื่อเล่น, acronym ก่อนตอบสนองทุกคำขอ
- อัปเดต CLAUDE.md (hot cache) และ memory/ (full storage) เมื่อมีข้อมูลใหม่
- จัดการ promotion/demotion ระหว่าง hot cache และ full storage

---

### `task-management` — จัดการ Task (Model-invoked, อัตโนมัติ)

**ไม่ต้องเรียกใช้เอง** — Claude โหลด skill นี้อัตโนมัติเมื่อคุณพูดถึงงาน

**สิ่งที่ทำ:**
- อ่านและเขียน TASKS.md
- เพิ่ม/mark done/ย้าย task ตามคำสั่ง
- ดึง task จากการสนทนาหรือการประชุม (พร้อมขอยืนยันก่อนเพิ่ม)

**Skills ทั้ง 4 ทำงานร่วมกัน:** `/start` สร้างระบบ → การใช้งานปกติ trigger `memory-management` และ `task-management` อัตโนมัติ → `/update` ซิงค์ทุกอย่างให้อยู่ปัจจุบัน

---

## โครงสร้างไฟล์ (Bilingual Design)

| ไฟล์/โฟลเดอร์ | ภาษา | ใช้โดย | วัตถุประสงค์ |
|---------------|------|--------|--------------|
| `skills/*/SKILL.md` | อังกฤษ + Thai directive | Claude | คำสั่งการทำงานหลัก (ลด token) |
| `skills/*/SKILL-TH.md` | ไทยทั้งหมด | ผู้ใช้ | เปิดอ่านทำความเข้าใจแต่ละ skill |
| `skills/dashboard.html` | — | Cowork | Template dashboard ที่ copy ไปยัง working directory |
| `CONNECTORS.md` | อังกฤษ | Claude | ข้อมูล MCP connector สำหรับ Claude |
| `CONNECTORS-TH.md` | ไทยทั้งหมด | ผู้ใช้ | คำแปลคู่มือการเชื่อมต่อเครื่องมือ |
| `.mcp.json` | — | Cowork | กำหนดค่า MCP server ล่วงหน้า |
| `.claude-plugin/plugin.json` | — | Cowork | Metadata ของ plugin |

---

## สัญญาอนุญาต (License)

### งานต้นฉบับ

ปลั๊กอินนี้ดัดแปลงมาจาก **productivity** โดย Anthropic, PBC ซึ่งเผยแพร่ภายใต้ **Apache License, Version 2.0**

```
Copyright Anthropic, PBC

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0
```

### งานดัดแปลง (Derivative Work)

**productivity (Localized)** เป็นงานดัดแปลง (Derivative Work) ตามนิยามของ Apache License 2.0 โดย **WARROOM-CEO** มีการเปลี่ยนแปลงดังนี้:

- เพิ่ม Thai Language Instruction Block ใน `SKILL.md` ทั้ง 4 ไฟล์: สั่งให้ Claude สื่อสารกับผู้ใช้เป็นภาษาไทย
- แปล `description` ใน frontmatter ของทุก `SKILL.md` เป็นภาษาไทย
- เพิ่มไฟล์ `SKILL-TH.md` ทั้ง 4 ไฟล์: คำแปลภาษาไทยเต็มรูปแบบสำหรับผู้ใช้อ่าน
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

*productivity (Localized) — ดัดแปลงจาก Anthropic productivity v1.2.0 โดย WARROOM-CEO*
