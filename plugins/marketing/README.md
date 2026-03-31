# marketing

**Plugin Marketing ครบวงจรสำหรับ Cowork — เวอร์ชันภาษาไทย**

Plugin นี้ช่วยให้คุณสร้างเนื้อหา วางแผน campaign วิเคราะห์คู่แข่ง ตรวจสอบ brand voice และรายงานผลการทำงานทุก marketing channel ทั้งหมดนี้สั่งงานได้ด้วยภาษาธรรมชาติ

---

## ภาพรวมการทำงาน

Plugin ทำงานผ่าน **Skills** สองรูปแบบ:

**Commands (User-invoked)** — workflow เฉพาะที่เรียกด้วย slash command เช่น `/draft-content`, `/campaign-plan`, `/brand-review` เหมาะสำหรับงานที่มีโครงสร้างและต้องการผลลัพธ์ที่ชัดเจน

**Skill (Model-invoked)** — `content-creation` ทำงานอัตโนมัติเป็น engine ภายในที่ Claude ใช้เมื่อสร้างหรือประเมิน marketing content ใน workflow ใดๆ ไม่ต้องพิมพ์ slash command

ตัวเชื่อมต่อ (Connectors) เช่น HubSpot, Ahrefs, Klaviyo, Amplitude เป็น optional — skills ทุกตัวทำงานได้แม้ไม่มี connector โดย Claude จะขอให้คุณให้ข้อมูลหรือค้นหาข้อมูลจากเว็บแทน

---

## Skills ทั้งหมด

### `/draft-content` — ร่าง Marketing Content (User-invoked)

**ใช้เมื่อ:** ต้องการเขียน marketing content ทุกประเภท

**สิ่งที่ทำ:** รับ content type, topic, audience และ key message → สร้าง draft ที่ format เหมาะกับ channel พร้อมคำแนะนำ SEO และ headline หลายตัวเลือก

**Trigger:** `/draft-content <ประเภทและหัวข้อ>`

**Content types:** Blog post, Social media (LinkedIn/Twitter/Instagram/Facebook), Email newsletter, Landing page, Press release, Case study

---

### `/campaign-plan` — วางแผน Campaign (User-invoked)

**ใช้เมื่อ:** ต้องการวางแผน marketing campaign ตั้งแต่ต้น

**สิ่งที่ทำ:** รับ goal, audience, timeline, budget → สร้าง campaign brief ครบถ้วน 10 sections รวม content calendar รายสัปดาห์พร้อม dependencies

**Trigger:** `/campaign-plan <objective หรือ product>`

**ความเชื่อมโยง:** ผลลัพธ์จาก campaign plan ส่งต่อไป `/draft-content` สำหรับสร้าง content จาก calendar ได้ทันที

---

### `/brand-review` — ตรวจสอบ Brand Voice (User-invoked)

**ใช้เมื่อ:** ต้องการตรวจสอบ content ก่อน publish หรือ audit copy เพื่อความสม่ำเสมอ

**สิ่งที่ทำ:** ตรวจสอบ content ตาม brand voice, style guide และ messaging pillar → แสดง finding ตาม severity (สูง/กลาง/ต่ำ) พร้อม before/after suggestion + legal flag

**Trigger:** `/brand-review <content ที่ต้องการตรวจสอบ>`

---

### `/competitive-brief` — วิเคราะห์คู่แข่ง (User-invoked)

**ใช้เมื่อ:** ต้องการ competitive analysis, สร้าง battlecard หรือหา positioning opportunity

**สิ่งที่ทำ:** ค้นหาข้อมูลคู่แข่งจากเว็บ → วิเคราะห์ messaging, content strategy, strengths/weaknesses → สร้าง positioning comparison, content gap analysis และ recommended actions

**Trigger:** `/competitive-brief <ชื่อคู่แข่ง หรือ market segment>`

---

### `/performance-report` — รายงานผลการทำงาน (User-invoked)

**ใช้เมื่อ:** ต้องการ marketing report รายสัปดาห์/เดือน/ไตรมาส หรือ campaign wrap-up

**สิ่งที่ทำ:** รวบรวม metric → วิเคราะห์ trend → ระบุ win/miss → ให้คำแนะนำ optimize ที่จัดลำดับตาม Impact vs Effort matrix

**Trigger:** `/performance-report <ช่วงเวลา หรือชื่อ campaign>`

---

### `/seo-audit` — ตรวจสอบ SEO (User-invoked)

**ใช้เมื่อ:** ต้องการประเมินสุขภาพ SEO, หา keyword opportunity หรือเปรียบเทียบ SEO กับคู่แข่ง

**สิ่งที่ทำ:** keyword research → on-page analysis → content gap → technical check → competitor comparison → แผนปฏิบัติการที่แบ่งเป็น quick win และ strategic investment

**Trigger:** `/seo-audit <URL หรือ topic> [ประเภท audit]`

---

### `/email-sequence` — ออกแบบ Email Sequence (User-invoked)

**ใช้เมื่อ:** ต้องการสร้าง drip campaign, onboarding, nurture flow หรือ win-back sequence

**สิ่งที่ทำ:** ออกแบบ sequence architecture → draft copy ทุก email พร้อม subject line options → กำหนด timing, branching logic, exit condition → สร้าง flow diagram + A/B test suggestions

**Trigger:** `/email-sequence [ประเภท sequence]`

---

### `content-creation` — คู่มือ Marketing Content (Model-invoked, อัตโนมัติ)

**Trigger:** อัตโนมัติเมื่อ Claude สร้างหรือประเมิน marketing content ใน workflow ใดๆ

**สิ่งที่ทำ:** เป็น internal knowledge base สำหรับ template, SEO fundamentals, headline formula, CTA best practice และ writing guidelines ทุก channel

**ความเชื่อมโยงระหว่าง Skills:** สกิลนี้ถูกอ้างอิงโดย `/draft-content`, `/campaign-plan`, `/brand-review` และ `/email-sequence` เมื่อสร้างเนื้อหา ไม่ใช้แบบ standalone

---

## โครงสร้างไฟล์ (Bilingual Design)

| ไฟล์/โฟลเดอร์ | ภาษา | ใช้โดย | วัตถุประสงค์ |
|---------------|------|--------|--------------|
| `skills/brand-review/SKILL.md` | อังกฤษ + Thai directive | Claude | คำสั่งการทำงาน brand-review |
| `skills/brand-review/SKILL-TH.md` | ไทยทั้งหมด | ผู้ใช้ | คำแปลภาษาไทยสำหรับผู้ใช้ |
| `skills/campaign-plan/SKILL.md` | อังกฤษ + Thai directive | Claude | คำสั่งการทำงาน campaign-plan |
| `skills/campaign-plan/SKILL-TH.md` | ไทยทั้งหมด | ผู้ใช้ | คำแปลภาษาไทยสำหรับผู้ใช้ |
| `skills/competitive-brief/SKILL.md` | อังกฤษ + Thai directive | Claude | คำสั่งการทำงาน competitive-brief |
| `skills/competitive-brief/SKILL-TH.md` | ไทยทั้งหมด | ผู้ใช้ | คำแปลภาษาไทยสำหรับผู้ใช้ |
| `skills/content-creation/SKILL.md` | อังกฤษ + Thai directive | Claude | คู่มือ content สำหรับ Claude (model-invoked) |
| `skills/content-creation/SKILL-TH.md` | ไทยทั้งหมด | ผู้ใช้ | คำแปลคู่มือ content |
| `skills/draft-content/SKILL.md` | อังกฤษ + Thai directive | Claude | คำสั่งการทำงาน draft-content |
| `skills/draft-content/SKILL-TH.md` | ไทยทั้งหมด | ผู้ใช้ | คำแปลภาษาไทยสำหรับผู้ใช้ |
| `skills/email-sequence/SKILL.md` | อังกฤษ + Thai directive | Claude | คำสั่งการทำงาน email-sequence |
| `skills/email-sequence/SKILL-TH.md` | ไทยทั้งหมด | ผู้ใช้ | คำแปลภาษาไทยสำหรับผู้ใช้ |
| `skills/performance-report/SKILL.md` | อังกฤษ + Thai directive | Claude | คำสั่งการทำงาน performance-report |
| `skills/performance-report/SKILL-TH.md` | ไทยทั้งหมด | ผู้ใช้ | คำแปลภาษาไทยสำหรับผู้ใช้ |
| `skills/seo-audit/SKILL.md` | อังกฤษ + Thai directive | Claude | คำสั่งการทำงาน seo-audit |
| `skills/seo-audit/SKILL-TH.md` | ไทยทั้งหมด | ผู้ใช้ | คำแปลภาษาไทยสำหรับผู้ใช้ |
| `CONNECTORS.md` | อังกฤษ | Claude | ข้อมูล connector สำหรับ Claude |
| `CONNECTORS-TH.md` | ไทยทั้งหมด | ผู้ใช้ | คำแปลคู่มือ connector |
| `.mcp.json` | — | Cowork | กำหนดค่า MCP server |
| `.claude-plugin/plugin.json` | — | Cowork | Metadata ของ plugin |

---

## สัญญาอนุญาต (License)

### งานต้นฉบับ

ปลั๊กอินนี้ดัดแปลงมาจาก **marketing** โดย Anthropic, PBC ซึ่งเผยแพร่ภายใต้ **Apache License, Version 2.0**

```
Copyright Anthropic, PBC

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0
```

### งานดัดแปลง (Derivative Work)

**marketing (Localized)** เป็นงานดัดแปลง (Derivative Work) ตามนิยามของ Apache License 2.0 โดย **WARROOM-CEO** มีการเปลี่ยนแปลงดังนี้:

- เพิ่ม Thai Language Instruction Block ใน `SKILL.md` ทั้ง 8 ไฟล์
- แปล `description` ใน frontmatter ของทุก skill เป็นภาษาไทย
- เพิ่มไฟล์ `SKILL-TH.md` สำหรับทุก skill (8 ไฟล์): คำแปลภาษาไทยสำหรับผู้ใช้
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

*marketing (Localized) — ดัดแปลงจาก Anthropic marketing v1.2.0 โดย WARROOM-CEO*
