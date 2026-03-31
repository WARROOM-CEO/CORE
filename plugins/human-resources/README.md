# Human Resources Plugin

เครื่องมือ AI สำหรับทีม HR และ People Operations — ออกแบบมาสำหรับ [Cowork](https://claude.com/product/cowork) แอปพลิเคชัน desktop ของ Anthropic และ Claude Code ช่วยเร่งกระบวนการสรรหาบุคลากร onboarding ประเมินผลการทำงาน วิเคราะห์ค่าตอบแทน และให้คำแนะนำด้านนโยบาย — ทำงานได้แบบ standalone หรือเชื่อมต่อ HRIS, ATS และเครื่องมืออื่นๆ เพื่อประสิทธิภาพสูงสุด

---

## ภาพรวมการทำงาน

Plugin นี้ครอบคลุมงาน people operations หลักทั้งหมด ทุก skill ทำงานได้โดยไม่ต้องเชื่อมต่อเครื่องมือ — เพียงให้ข้อมูลที่ต้องการ และจะทำงานได้ดีขึ้นอีกเมื่อเชื่อมต่อ HRIS, ATS และระบบอื่นๆ

**สรรหาบุคลากร** — `recruiting-pipeline` ติดตาม pipeline ตั้งแต่ sourcing ถึง offer accepted, `interview-prep` สร้างแผนสัมภาษณ์ที่ structured และ fair, `draft-offer` ร่าง offer letter พร้อม total comp package

**Onboarding** — `onboarding` สร้างแผนครบถ้วน pre-start → Day 1 → Week 1 → 30/60/90-day goals พร้อมตาราง tool access

**ประเมินผล** — `performance-review` สร้าง self-assessment template, manager review และ calibration prep ให้ feedback ที่เจาะจงและ actionable

**ค่าตอบแทน** — `comp-analysis` เปรียบเทียบกับตลาด จัดวาง band placement และ model equity refresh grant

**People Analytics** — `people-report` สร้างรายงาน headcount, attrition, diversity และ org health จาก data ที่อัปโหลดหรือ HRIS

**นโยบายและ Compliance** — `policy-lookup` ตอบคำถาม HR ด้วยภาษาที่เข้าใจง่าย อ้างอิง source จริง

---

## Skills ทั้งหมด

| Skill | ประเภท | Trigger | เชื่อมโยงกับ |
|-------|--------|---------|-------------|
| `draft-offer` | User-invoked | `/draft-offer <role and level>` | `comp-analysis` (ตรวจสอบ band ก่อน offer) |
| `onboarding` | User-invoked | `/onboarding <ชื่อและ role>` | — |
| `performance-review` | User-invoked | `/performance-review <ชื่อหรือ cycle>` | — |
| `policy-lookup` | User-invoked | `/policy-lookup <หัวข้อ>` | — |
| `comp-analysis` | User-invoked | `/comp-analysis <role, level, หรือ dataset>` | — |
| `people-report` | User-invoked | `/people-report <ประเภทรายงาน>` | — |
| `recruiting-pipeline` | Model-invoked | เรียกอัตโนมัติเมื่อพูดถึง recruiting/hiring | `interview-prep`, `draft-offer` |
| `interview-prep` | Model-invoked | เรียกอัตโนมัติเมื่อเตรียมสัมภาษณ์ candidate | `recruiting-pipeline` |
| `org-planning` | Model-invoked | เรียกอัตโนมัติเมื่อพูดถึง headcount/org design | `comp-analysis` (cost modeling) |

### รายละเอียด Skills

**`draft-offer`** — ร่าง offer letter ครบชุดพร้อม compensation package (base, equity, signing bonus, total comp), เงื่อนไขการจ้างงาน, สรุปสวัสดิการ และ guidance การเจรจาสำหรับ hiring manager

**`onboarding`** — สร้างแผน onboarding ที่ customize ตาม role: pre-start checklist, ตาราง Day 1 ชั่วโมงต่อชั่วโมง, Week 1 tasks, เป้าหมาย 30/60/90 วัน, รายชื่อ key contacts และ tool access list

**`performance-review`** — 3 โหมด: Self-Assessment Template (พนักงานเขียนเอง), Manager Review Template (manager เขียนให้ direct report) และ Calibration Prep (เตรียม calibration session พร้อม rating distribution)

**`policy-lookup`** — ค้นหาและอธิบาย policy ด้วยภาษาที่เข้าใจง่าย ครอบคลุม PTO, สวัสดิการ, remote work, travel, ค่าใช้จ่าย และ code of conduct พร้อมอ้างอิง source จริง

**`comp-analysis`** — วิเคราะห์ค่าตอบแทน 3 แบบ: เปรียบเทียบตลาดรายตำแหน่ง (percentile 25th-90th), วิเคราะห์ band placement จากข้อมูลที่อัปโหลด และ model equity grant

**`people-report`** — รายงาน 4 ประเภท: Headcount, Attrition, Diversity และ Org Health พร้อม executive summary, ตัวชี้วัดหลัก, การวิเคราะห์เชิงลึก และคำแนะนำ

**`recruiting-pipeline`** *(Model-invoked)* — ติดตาม pipeline 6 ขั้นตอน (Sourced → Screen → Interview → Debrief → Offer → Accepted) พร้อม conversion metrics และ velocity tracking

**`interview-prep`** *(Model-invoked)* — สร้าง interview kit ครบชุด: panel assignment, question bank ตาม competency, scoring rubric 1-4 และ debrief template

**`org-planning`** *(Model-invoked)* — วางแผน headcount, ออกแบบ org structure, จัด hiring roadmap และ flag ปัญหาโครงสร้าง เช่น single points of failure หรือ management overhead สูงเกินไป

---

## โครงสร้างไฟล์ — Bilingual Design

| ไฟล์ (English — Claude ใช้) | ไฟล์ (Thai — ผู้ใช้อ่าน) | วัตถุประสงค์ |
|---------------------------|------------------------|-------------|
| `skills/draft-offer/SKILL.md` | `skills/draft-offer/SKILL-TH.md` | ร่าง offer letter |
| `skills/onboarding/SKILL.md` | `skills/onboarding/SKILL-TH.md` | แผน onboarding พนักงานใหม่ |
| `skills/performance-review/SKILL.md` | `skills/performance-review/SKILL-TH.md` | ประเมินผลการทำงาน |
| `skills/policy-lookup/SKILL.md` | `skills/policy-lookup/SKILL-TH.md` | ค้นหา company policy |
| `skills/comp-analysis/SKILL.md` | `skills/comp-analysis/SKILL-TH.md` | วิเคราะห์ค่าตอบแทน |
| `skills/people-report/SKILL.md` | `skills/people-report/SKILL-TH.md` | รายงาน people analytics |
| `skills/recruiting-pipeline/SKILL.md` | `skills/recruiting-pipeline/SKILL-TH.md` | บริหาร recruiting pipeline (Model-invoked) |
| `skills/interview-prep/SKILL.md` | `skills/interview-prep/SKILL-TH.md` | เตรียมแผนสัมภาษณ์ (Model-invoked) |
| `skills/org-planning/SKILL.md` | `skills/org-planning/SKILL-TH.md` | วางแผนองค์กรและ headcount (Model-invoked) |
| `CONNECTORS.md` | `CONNECTORS-TH.md` | รายการ MCP connectors |
| `README.md` *(ไฟล์นี้)* | — | ภาพรวม plugin ภาษาไทย |

---

## สัญญาอนุญาต

Plugin นี้ใช้สัญญาอนุญาต **Apache License 2.0**

**ต้นฉบับ**: จัดทำโดย Anthropic — ดูไฟล์ `LICENSE` สำหรับรายละเอียดฉบับสมบูรณ์

**งานดัดแปลง (Derivative Works)**: หากองค์กรปรับแต่ง plugin นี้ (เช่น เพิ่ม skills, ปรับ comp bands หรือแก้ไข templates) ถือเป็นงานดัดแปลงภายใต้ Apache 2.0

| สิทธิ์ | รายละเอียด |
|--------|-----------|
| ✅ ใช้งานเชิงพาณิชย์ | ใช้ได้ในองค์กรทุกประเภท |
| ✅ ดัดแปลง | ปรับแต่ง skills และ templates ได้ตามต้องการ |
| ✅ แจกจ่าย | แชร์เวอร์ชันดัดแปลงได้ภายใต้เงื่อนไขเดิม |
| ✅ ใช้สิทธิบัตร | ได้รับสิทธิ์ใช้งานสิทธิบัตรที่เกี่ยวข้องจาก Anthropic |
| ❌ การรับประกัน | ไม่มีการรับประกัน ใช้งานตามความเสี่ยงของตนเอง |
| ❌ ความรับผิด | Anthropic ไม่รับผิดชอบต่อความเสียหายจากการใช้งาน |
