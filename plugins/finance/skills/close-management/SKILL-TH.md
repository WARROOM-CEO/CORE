# Skill: close-management — บริหาร Month-End Close

**ประเภท**: Model-invoked — เรียกอัตโนมัติเมื่อพูดถึง month-end close, close calendar, close progress หรือการจัดลำดับ close activities

> **ข้อสงวนสิทธิ์**: Skill นี้ช่วยในงาน close management workflow แต่ไม่ได้ให้คำแนะนำทางการเงิน ทุก close activities ควรได้รับการตรวจสอบโดยผู้เชี่ยวชาญ

---

## ขอบเขตความรู้

Skill นี้ครอบคลุม:
- Month-end close checklist แบบครบวงจร
- Task sequencing และ dependencies ระหว่าง close activities
- Status tracking และการระบุ blockers
- Close activities จัดตาม Day ของ close

---

## โครงสร้าง Close Process

### Pre-Close (2-3 Business Days ก่อนสิ้นเดือน)
- ส่ง close calendar และ deadline reminders ให้ทุก contributor
- ยืนยัน cut-off procedures กับ AP, AR, payroll และ treasury
- ตรวจสอบว่า sub-systems ทำงานปกติ (ERP, payroll, banking)
- ทำ bank reconciliation เบื้องต้น (ยกเว้น activity วันสุดท้าย)
- ทบทวน open purchase orders สำหรับ accrual ที่อาจจำเป็น

### Close Day 1-2
- บันทึก journal entries หลัก (accruals, prepaids, depreciation, payroll)
- ปิด sub-systems และล็อค transaction periods
- เริ่ม account reconciliations

### Close Day 3-5
- สรุป reconciliations ทั้งหมดและแก้ไข reconciling items
- ทำ intercompany eliminations
- Review journal entries — approval ตาม threshold
- ทำ preliminary financial statements

### Post-Close
- Management review ของ financial statements
- Variance analysis และ flux commentary
- รายงานต่อ leadership และส่งต่อ audit

---

## Close Status Tracking

| งาน | Owner | Due | Status | Blockers |
|-----|-------|-----|--------|---------|
| AP Accruals | [ชื่อ] | Day 1 | [Not Started / In Progress / Complete] | [ถ้ามี] |
| Payroll JE | [ชื่อ] | Day 1 | | |
| Bank Rec | [ชื่อ] | Day 2 | | |
| AR Rec | [ชื่อ] | Day 3 | | |
| Financial Statements | [ชื่อ] | Day 5 | | |
| Management Review | [ชื่อ] | Day 6 | | |

---

## Close Metrics ที่ควรวัด

**Close duration** — จำนวนวันจาก Day 1 ถึง financial statements ที่ approved

**Late items** — จำนวน items ที่ส่งเกิน deadline

**Post-close adjustments** — JE ที่ต้องบันทึกหลัง close แสดงถึงปัญหา cut-off

**Reconciling items aging** — รายการที่ค้างมากกว่า 30 วันใน reconciliations
