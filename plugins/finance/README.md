# Finance & Accounting Plugin

เครื่องมือ AI สำหรับทีม Finance และ Accounting — ออกแบบมาสำหรับ [Cowork](https://claude.com/product/cowork) แอปพลิเคชัน desktop ของ Anthropic และ Claude Code ครอบคลุม month-end close, journal entry preparation, account reconciliation, financial statements, variance analysis และ SOX audit support

> **ข้อสงวนสิทธิ์**: Plugin นี้ช่วยในงาน finance และ accounting workflow แต่ไม่ได้ให้คำแนะนำทางการเงิน ภาษี หรือ audit ทุก output ควรได้รับการตรวจสอบโดยผู้เชี่ยวชาญก่อนนำไปใช้ใน financial reporting, regulatory filings หรือ audit documentation

---

## ภาพรวมการทำงาน

Plugin นี้ออกแบบมาสำหรับ finance team ที่ต้องการเพิ่มความเร็วและความแม่นยำใน accounting workflows สำคัญ ทุก skill ทำงานได้แบบ standalone — เพียงวางข้อมูลหรืออัปโหลดไฟล์ และจะทำงานได้ดีขึ้นอีกมากเมื่อเชื่อมต่อกับ ERP, data warehouse และระบบอื่นๆ

**Month-End Close** — `close-management` จัดลำดับงาน close ตาม day พร้อม dependencies และ status tracking ช่วยให้ close เสร็จเร็วขึ้นและมีน้อยลงที่ตกหล่น

**Journal Entries** — `/journal-entry` สร้าง JE ที่ถูกต้องทุกประเภท (accruals, prepaids, depreciation, payroll, revenue recognition) พร้อม supporting documentation template

**Reconciliation** — `/reconciliation` กระทบยอด GL กับ subledger, bank หรือ third-party data ระบุ reconciling items พร้อม aging analysis

**Financial Statements** — `/financial-statements` สร้าง P&L, Balance Sheet, Cash Flow พร้อม period-over-period comparison และ flag material variances

**Variance Analysis** — `/variance-analysis` แยกวิเคราะห์ variances ตาม drivers พร้อม waterfall chart และ narrative commentary สำหรับ management

**SOX Compliance** — `/sox-testing` สร้าง sample selections, workpapers และ control assessments; `audit-support` ให้ความรู้ SOX methodology อัตโนมัติ

---

## Skills ทั้งหมด

| Skill | ประเภท | Trigger | เชื่อมโยงกับ |
|-------|--------|---------|-------------|
| `journal-entry` | User-invoked | `/journal-entry <entry type> [period]` | `journal-entry-prep` (best practices) |
| `reconciliation` | User-invoked | `/reconciliation <account> [period]` | — |
| `financial-statements` | User-invoked | `/financial-statements <frequency> <period>` | `variance-analysis` (flag variances) |
| `variance-analysis` | User-invoked | `/variance-analysis <line item> <period> vs <comparison>` | — |
| `sox-testing` | User-invoked | `/sox-testing <control area> [period]` | `audit-support` (methodology) |
| `journal-entry-prep` | Model-invoked | เรียกอัตโนมัติเมื่อเตรียม journal entries | `journal-entry` |
| `close-management` | Model-invoked | เรียกอัตโนมัติเมื่อพูดถึง month-end close | `journal-entry`, `reconciliation` |
| `audit-support` | Model-invoked | เรียกอัตโนมัติเมื่อพูดถึง SOX, audit preparation | `sox-testing` |

### รายละเอียด Skills

**`journal-entry`** — เตรียม journal entries ครบชุดพร้อม debit/credit table, account codes, supporting documentation list และ review notes สำหรับทุกประเภท entry (AP accrual, prepaid, depreciation, payroll, revenue recognition)

**`reconciliation`** — กระทบยอด 4 ประเภท: Bank Rec, GL-to-Subledger, Intercompany, Third-Party พร้อม reconciling items table, aging summary และ required actions

**`financial-statements`** — สร้าง P&L, Balance Sheet หรือ Cash Flow พร้อมตาราง period-over-period comparison, variance % และ flag รายการที่มีนัยสำคัญ (>5% หรือ >$50K)

**`variance-analysis`** — Waterfall analysis แสดง drivers ของ variance (volume, price/rate, mix) พร้อม narrative summary 2-3 ประโยคสำหรับ management และ action items

**`sox-testing`** — สร้าง workpaper templates ครบชุดตาม control area (Revenue, P2P, Payroll, ITGC, Close, Fixed Assets, Treasury) พร้อม sample selection guidance และ deficiency classification

**`journal-entry-prep`** *(Model-invoked)* — ความรู้ best practices JE preparation: ประเภท accruals มาตรฐาน, supporting documentation requirements, review workflows และ common errors ที่ต้องระวัง

**`close-management`** *(Model-invoked)* — Month-end close checklist จัดตาม Day, task dependencies, status tracking template และ close metrics ที่ควรวัด

**`audit-support`** *(Model-invoked)* — SOX 404 methodology ครบชุด: scoping, risk assessment, sample selection, documentation standards, control deficiency classification และ common control types (ITGC, Manual, Automated, Entity-Level)

---

## โครงสร้างไฟล์ — Bilingual Design

| ไฟล์ (English — Claude ใช้) | ไฟล์ (Thai — ผู้ใช้อ่าน) | วัตถุประสงค์ |
|---------------------------|------------------------|-------------|
| `skills/journal-entry/SKILL.md` | `skills/journal-entry/SKILL-TH.md` | เตรียม journal entries |
| `skills/reconciliation/SKILL.md` | `skills/reconciliation/SKILL-TH.md` | กระทบยอดบัญชี |
| `skills/financial-statements/SKILL.md` | `skills/financial-statements/SKILL-TH.md` | สร้าง financial statements |
| `skills/variance-analysis/SKILL.md` | `skills/variance-analysis/SKILL-TH.md` | วิเคราะห์ variance |
| `skills/sox-testing/SKILL.md` | `skills/sox-testing/SKILL-TH.md` | SOX compliance testing |
| `skills/journal-entry-prep/SKILL.md` | `skills/journal-entry-prep/SKILL-TH.md` | ความรู้ JE preparation (Model-invoked) |
| `skills/close-management/SKILL.md` | `skills/close-management/SKILL-TH.md` | บริหาร month-end close (Model-invoked) |
| `skills/audit-support/SKILL.md` | `skills/audit-support/SKILL-TH.md` | SOX audit methodology (Model-invoked) |
| `CONNECTORS.md` | `CONNECTORS-TH.md` | รายการ MCP connectors |
| `README.md` *(ไฟล์นี้)* | — | ภาพรวม plugin ภาษาไทย |

---

## สัญญาอนุญาต

Plugin นี้ใช้สัญญาอนุญาต **Apache License 2.0**

**ต้นฉบับ**: จัดทำโดย Anthropic — ดูไฟล์ `LICENSE` สำหรับรายละเอียดฉบับสมบูรณ์

**งานดัดแปลง (Derivative Works)**: หากองค์กรปรับแต่ง plugin นี้ (เช่น เพิ่ม control areas, ปรับ materiality thresholds หรือแก้ไข templates) ถือเป็นงานดัดแปลงภายใต้ Apache 2.0

| สิทธิ์ | รายละเอียด |
|--------|-----------|
| ✅ ใช้งานเชิงพาณิชย์ | ใช้ได้ในองค์กรทุกประเภท |
| ✅ ดัดแปลง | ปรับแต่ง skills และ templates ได้ตามต้องการ |
| ✅ แจกจ่าย | แชร์เวอร์ชันดัดแปลงได้ภายใต้เงื่อนไขเดิม |
| ✅ ใช้สิทธิบัตร | ได้รับสิทธิ์ใช้งานสิทธิบัตรที่เกี่ยวข้องจาก Anthropic |
| ❌ การรับประกัน | ไม่มีการรับประกัน ใช้งานตามความเสี่ยงของตนเอง |
| ❌ ความรับผิด | Anthropic ไม่รับผิดชอบต่อความเสียหายจากการใช้งาน |
