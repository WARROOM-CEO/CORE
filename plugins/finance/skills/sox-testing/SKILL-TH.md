# Skill: sox-testing — SOX Compliance Testing

**ประเภท**: User-invoked — `/sox-testing <control area> [period]`

สร้าง SOX sample selections, testing workpapers และ control assessments สำหรับ SOX 404 compliance

> **ข้อสงวนสิทธิ์**: Plugin นี้ช่วยในงาน SOX compliance workflow แต่ไม่ได้ให้คำแนะนำด้าน audit หรือกฎหมาย ทุก testing workpaper และการประเมินควรได้รับการตรวจสอบโดยผู้เชี่ยวชาญก่อนนำไปใช้

---

## วิธีเรียกใช้

```
/sox-testing revenue-recognition 2025-Q1
/sox-testing procure-to-pay 2025-Q4
/sox-testing itgc 2025-annual
/sox-testing financial-close 2025-Q3
/sox-testing access-controls 2025-Q2
```

---

## Control Areas ที่รองรับ

| Control Area | Placeholder | Controls หลัก |
|-------------|-------------|--------------|
| Revenue Recognition | `revenue` | Order-to-cash, cut-off, deferred revenue |
| Procure-to-Pay | `procure-to-pay` / `p2p` | PO approval, three-way match, vendor setup |
| Payroll | `payroll` | Employee master changes, payroll processing, approval |
| Financial Close | `close` | Journal entry approval, reconciliations, management review |
| IT General Controls | `itgc` | Access provisioning, change management, operations |
| Fixed Assets | `fixed-assets` | Additions, disposals, depreciation, impairment |
| Treasury/Cash | `treasury` | Bank account setup, wire transfer approval, cash reconciliation |

---

## Sample Size Guidance

| ความถี่ Control | Population | Low Risk | Medium Risk | High Risk |
|----------------|-----------|----------|-------------|-----------|
| Annual | 1 | 1 | 1 | 1 |
| Quarterly | 4 | 2 | 2 | 3 |
| Monthly | 12 | 2 | 3 | 4 |
| Weekly | 52 | 5 | 8 | 15 |
| Daily | ~250 | 20 | 30 | 40 |
| Per-transaction | 250+ | 25 | 40 | 60 |

---

## รูปแบบ Testing Workpaper

```
## SOX Testing Workpaper: [Control Name]
Period: [Q] | Control Area: [Area] | Risk Level: [Low/Medium/High]

### Control Description
[สิ่งที่ control ทำ, ใครเป็นผู้ดำเนินการ, ความถี่, ประเภท (Manual/Automated/IT-Dependent Manual)]

### Risk & Assertion Addressed
[Risk ที่ control นี้ address และ PCAOB assertion]

### Test Design
| Test Objective | Test Procedures | Expected Evidence |
|---------------|----------------|-------------------|

### Sample Selection
| Method | Population Size | Sample Size | Rationale |
|--------|----------------|-------------|-----------|

### Test Results
| Sample # | Item | Result | Evidence | Exception Notes |
|----------|------|--------|----------|----------------|

### Conclusion
[ ] Effective  [ ] Deficiency  [ ] Significant Deficiency  [ ] Material Weakness
Basis: [เหตุผล]
```

---

## การจำแนก Control Deficiency

**Deficiency** — Control ไม่ทำงานตามที่ออกแบบ แต่ความน่าจะเป็นของ material misstatement ต่ำ

**Significant Deficiency** — สำคัญพอที่ควรได้รับความสนใจจาก governance แต่ยังไม่ถึงขั้น material weakness

**Material Weakness** — มีความน่าจะเป็นสมเหตุสมผลที่จะเกิด material misstatement ที่ไม่ถูกป้องกันหรือตรวจพบ

---

## การเชื่อมต่อที่ช่วยเพิ่มประสิทธิภาพ

เมื่อเชื่อมต่อ **~~erp** — ดึงรายการ transactions สำหรับ sample selection อัตโนมัติ

เมื่อเชื่อมต่อ **~~office suite** — สร้าง workpaper templates ใน Excel หรือ Word ที่พร้อมใช้งาน
