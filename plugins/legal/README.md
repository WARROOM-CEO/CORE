# Legal Productivity Plugin

เครื่องมือ AI สำหรับทีม legal ภายในองค์กร — ออกแบบมาสำหรับ [Cowork](https://claude.com/product/cowork) แอปพลิเคชัน desktop ของ Anthropic และ Claude Code ช่วยเร่งกระบวนการตรวจสอบสัญญา คัดกรอง NDA ตรวจสอบ compliance ร่าง brief และจัดการ response ตามเทมเพลต — ทั้งหมดปรับแต่งได้ตาม playbook และระดับความเสี่ยงขององค์กร

> **ข้อสงวนสิทธิ์**: Plugin นี้ช่วยในงาน legal workflow แต่ไม่ได้ให้คำแนะนำทางกฎหมาย การวิเคราะห์ทั้งหมดควรได้รับการตรวจสอบโดยผู้เชี่ยวชาญด้านกฎหมายที่มีคุณวุฒิ ตัวอย่างใน playbook เริ่มต้นอ้างอิงตำแหน่งและเขตอำนาจศาลของสหรัฐอเมริกา หากองค์กรอยู่ภายใต้ระบบกฎหมายอื่น (EU, UK, ออสเตรเลีย ฯลฯ) ต้องปรับแต่ง playbook ใน `legal.local.md` ก่อนนำไปใช้งานจริง

---

## ภาพรวมการทำงาน

Plugin นี้รองรับบทบาท legal ภายในองค์กร 4 กลุ่มหลัก:

**Commercial Counsel** ใช้ `/review-contract` และ `/vendor-check` เพื่อเจรจาสัญญา บริหารความสัมพันธ์กับ vendor และสนับสนุน deal team ได้รวดเร็วขึ้น

**Product Counsel** ใช้ `/triage-nda` และ `/review-contract` เพื่อคัดกรองสัญญาที่เข้ามา ตรวจสอบ Terms of Service นโยบายความเป็นส่วนตัว และประเด็น IP

**Privacy / Compliance** ใช้ `/compliance-check` เพื่อตรวจสอบ GDPR, CCPA/CPRA และ DPA พร้อม gap analysis และ action items ที่ชัดเจน

**Litigation Support** ใช้ `/brief` เพื่อเตรียม briefing สำหรับการประชุมและ incident ที่เกิดขึ้น พร้อม context ครบถ้วน

Plugin ทำงานได้ดีที่สุดเมื่อเชื่อมต่อกับ CLM, email, cloud storage, chat และ e-signature — แต่ gracefully degrade เมื่อเครื่องมือบางส่วนไม่ได้เชื่อมต่อ

---

## Skills ทั้งหมด

| Skill | ประเภท | Trigger | เชื่อมโยงกับ |
|-------|--------|---------|-------------|
| `review-contract` | User-invoked | `/review-contract [ไฟล์/URL/ข้อความ]` | `legal-risk-assessment` (ประเมินความเสี่ยงอัตโนมัติ) |
| `triage-nda` | User-invoked | `/triage-nda [NDA]` | `review-contract` (ถ้า RED ส่งต่อเพื่อ full review) |
| `vendor-check` | User-invoked | `/vendor-check [ชื่อ vendor]` | `review-contract` (ตรวจสอบสัญญาที่พบ) |
| `brief` | User-invoked | `/brief daily` / `/brief topic [หัวข้อ]` / `/brief incident` | `meeting-briefing` (ใช้ methodology เดียวกัน) |
| `legal-response` | User-invoked | `/respond [ประเภท inquiry]` | — |
| `compliance-check` | User-invoked | `/compliance-check [ระบบ/กระบวนการ]` | `legal-risk-assessment` (ประเมิน risk ของ gap ที่พบ) |
| `signature-request` | User-invoked | `/signature-request [เอกสาร]` | — |
| `legal-risk-assessment` | Model-invoked | เรียกอัตโนมัติโดย `review-contract` และ `compliance-check` | — |
| `meeting-briefing` | Model-invoked | เรียกอัตโนมัติเมื่อตรวจพบ legal meeting ใน calendar | — |

### รายละเอียด Skills

**`review-contract`** — ตรวจสอบสัญญาตาม negotiation playbook ขององค์กร วิเคราะห์แต่ละ clause และจำแนกเป็น GREEN (ยอมรับได้), YELLOW (ต้องเจรจา) หรือ RED (ต้อง escalate) พร้อม redline ที่เจาะจงและ business impact analysis

**`triage-nda`** — คัดกรอง NDA ที่เข้ามาตาม 10 เกณฑ์มาตรฐาน จำแนกเป็น GREEN (อนุมัติมาตรฐาน), YELLOW (ทบทวนโดย counsel) หรือ RED (มีปัญหาสำคัญ ต้อง full legal review)

**`vendor-check`** — ค้นหาสถานะสัญญาที่มีอยู่กับ vendor ทั่วทุกระบบที่เชื่อมต่อ สร้างมุมมองรวมพร้อม gap analysis (NDA, MSA, DPA, SOW, SLA) และ deadline ที่ใกล้ถึง

**`brief`** — สร้าง briefing 3 โหมด: Daily Brief (สรุปสิ่งที่ต้องดูแลในวันนี้), Topic Brief (วิเคราะห์ประเด็น legal เฉพาะ) และ Incident Brief (สรุปสถานการณ์ฉุกเฉินอย่างรวดเร็ว)

**`legal-response`** — สร้าง response ตามเทมเพลตสำหรับ inquiry ทั่วไป เช่น data subject request, discovery hold, vendor inquiry, NDA request พร้อม escalation trigger อัตโนมัติ

**`compliance-check`** — ตรวจสอบ compliance กับ GDPR, CCPA/CPRA และ regulation อื่นๆ ระบุ gap พร้อม action items ที่ชัดเจน และประเมิน risk ของแต่ละ gap

**`signature-request`** — เตรียมและส่งเอกสารเพื่อลงลายเซ็น e-signature ตรวจสอบ pre-signature checklist กำหนด signing order และส่งผ่าน DocuSign, Adobe Sign หรือระบบที่เชื่อมต่อ

**`legal-risk-assessment`** *(Model-invoked)* — ประเมินความเสี่ยงด้วย Severity × Likelihood matrix จำแนกเป็น 4 ระดับ (GREEN/YELLOW/ORANGE/RED) เรียกใช้อัตโนมัติโดย skills อื่น

**`meeting-briefing`** *(Model-invoked)* — เตรียม briefing สำหรับ legal meeting โดยรวบรวม context จากทุกระบบที่เชื่อมต่อ ติดตาม action item และ follow-up ที่ค้างอยู่

---

## โครงสร้างไฟล์ — Bilingual Design

| ไฟล์ (English — Claude ใช้) | ไฟล์ (Thai — ผู้ใช้อ่าน) | วัตถุประสงค์ |
|---------------------------|------------------------|-------------|
| `skills/review-contract/SKILL.md` | `skills/review-contract/SKILL-TH.md` | ตรวจสอบสัญญาตาม playbook |
| `skills/triage-nda/SKILL.md` | `skills/triage-nda/SKILL-TH.md` | คัดกรอง NDA 10 เกณฑ์ |
| `skills/vendor-check/SKILL.md` | `skills/vendor-check/SKILL-TH.md` | ตรวจสอบสถานะสัญญา vendor |
| `skills/brief/SKILL.md` | `skills/brief/SKILL-TH.md` | สร้าง briefing 3 โหมด |
| `skills/legal-response/SKILL.md` | `skills/legal-response/SKILL-TH.md` | Response ตามเทมเพลต |
| `skills/compliance-check/SKILL.md` | `skills/compliance-check/SKILL-TH.md` | ตรวจสอบ GDPR/CCPA compliance |
| `skills/signature-request/SKILL.md` | `skills/signature-request/SKILL-TH.md` | ส่งเอกสารเพื่อลงลายเซ็น |
| `skills/legal-risk-assessment/SKILL.md` | `skills/legal-risk-assessment/SKILL-TH.md` | ประเมินความเสี่ยง (Model-invoked) |
| `skills/meeting-briefing/SKILL.md` | `skills/meeting-briefing/SKILL-TH.md` | เตรียม meeting (Model-invoked) |
| `CONNECTORS.md` | `CONNECTORS-TH.md` | รายการ MCP connectors |
| `README.md` *(ไฟล์นี้)* | — | ภาพรวม plugin ภาษาไทย |

---

## สัญญาอนุญาต

Plugin นี้ใช้สัญญาอนุญาต **Apache License 2.0**

**ต้นฉบับ**: จัดทำโดย Anthropic — ดูไฟล์ `LICENSE` สำหรับรายละเอียดฉบับสมบูรณ์

**งานดัดแปลง (Derivative Works)**: หากองค์กรปรับแต่ง plugin นี้ (เช่น แก้ไข playbook ใน `legal.local.md` หรือดัดแปลง skills) ถือเป็นงานดัดแปลงภายใต้ Apache 2.0

| สิทธิ์ | รายละเอียด |
|--------|-----------|
| ✅ ใช้งานเชิงพาณิชย์ | ใช้ได้ในองค์กรทุกประเภท |
| ✅ ดัดแปลง | ปรับแต่ง playbook และ skills ได้ตามต้องการ |
| ✅ แจกจ่าย | แชร์เวอร์ชันดัดแปลงได้ภายใต้เงื่อนไขเดิม |
| ✅ ใช้สิทธิบัตร | ได้รับสิทธิ์ใช้งานสิทธิบัตรที่เกี่ยวข้องจาก Anthropic |
| ❌ การรับประกัน | ไม่มีการรับประกัน ใช้งานตามความเสี่ยงของตนเอง |
| ❌ ความรับผิด | Anthropic ไม่รับผิดชอบต่อความเสียหายจากการใช้งาน |
