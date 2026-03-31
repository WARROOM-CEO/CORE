# Skill: audit-support — สนับสนุน SOX Audit

**ประเภท**: Model-invoked — เรียกอัตโนมัติเมื่อพูดถึง SOX compliance, control testing, audit preparation, หรือ deficiency classification

> **ข้อสงวนสิทธิ์**: Skill นี้ช่วยในงาน SOX compliance workflow แต่ไม่ได้ให้คำแนะนำด้าน audit หรือกฎหมาย ความหมายของ "materiality" และ "significance" ขึ้นอยู่กับบริบทและต้องได้รับการประเมินโดย auditor ที่มีคุณวุฒิ

---

## ขอบเขตความรู้

Skill นี้ครอบคลุม:
- SOX 404 control testing methodology (scoping, risk assessment, control identification, testing, evaluation, reporting)
- Sample selection approaches (random, targeted/judgmental, haphazard, systematic)
- Testing documentation standards — workpaper requirements และ evidence standards
- Control deficiency classification (Deficiency, Significant Deficiency, Material Weakness)
- Common control types (ITGC, Manual Controls, Automated Controls, IT-Dependent Manual Controls, Entity-Level Controls)

---

## กระบวนการ SOX 404

**Scoping** → ระบุ significant accounts และ relevant assertions

**Risk Assessment** → ประเมิน risk of material misstatement สำหรับแต่ละ account

**Control Identification** → document controls ที่ address แต่ละ risk

**Testing** → ทดสอบ design effectiveness และ operating effectiveness ของ key controls

**Evaluation** → ประเมินว่ามี deficiencies หรือไม่ และระดับความรุนแรง

**Reporting** → document การประเมินและ material weaknesses ที่พบ

---

## การจำแนก Control Deficiency

| ระดับ | นิยาม | ตัวชี้วัด |
|------|------|---------|
| **Deficiency** | Control ไม่ทำงานตามที่ออกแบบ | ความน่าจะเป็นของ misstatement ต่ำ |
| **Significant Deficiency** | สำคัญพอที่ governance ต้องให้ความสนใจ | ความน่าจะเป็นระดับกลาง |
| **Material Weakness** | มีความน่าจะเป็นสมเหตุสมผลของ material misstatement | สูง — ต้องรายงานต่อ audit committee |

**สัญญาณของ Material Weakness:** การทุจริตโดย senior management, restatement ของ financial statements, auditor พบ misstatement ที่ internal controls ตรวจไม่พบ, การควบคุมโดย audit committee ที่ไม่มีประสิทธิภาพ

---

## ประเภท Controls

**IT General Controls (ITGC)** — Access provisioning/deprovisioning, privileged access management, change management, IT operations (batch jobs, backup/recovery, incident management)

**Manual Controls** — Management review, supervisory approval, three-way match, account reconciliation, physical inventory — ทดสอบโดยดูว่าใครทำ, ทำตรงเวลา, มีหลักฐาน และมีข้อมูลพอที่จะ review ได้จริง

**Automated Controls** — System-enforced workflows, duplicate payment detection, credit limit enforcement — ถ้า system ไม่เปลี่ยนแปลง ทดสอบครั้งเดียวต่อปีก็เพียงพอ

**IT-Dependent Manual Controls** — Manual controls ที่พึ่งพา system-generated reports — ต้องทดสอบทั้ง control และ IPE (Information Produced by the Entity)

**Entity-Level Controls** — Tone at the top, audit committee oversight, risk assessment process, fraud risk assessment — ถ้า ineffective อาจเป็น indicator ของ material weakness
