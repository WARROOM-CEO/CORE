# Skill: journal-entry-prep — ความรู้การเตรียม Journal Entry

**ประเภท**: Model-invoked — เรียกอัตโนมัติเมื่อมีการเตรียม journal entries โดย `/journal-entry` หรือเมื่อพูดถึง accruals, JE preparation, month-end entries

> **ข้อสงวนสิทธิ์**: Skill นี้ช่วยในงาน accounting workflow แต่ไม่ได้ให้คำแนะนำทางการเงิน ทุก journal entries ควรได้รับการตรวจสอบโดยผู้เชี่ยวชาญก่อน post

---

## ขอบเขตความรู้

Skill นี้ครอบคลุม:
- Best practices การเตรียม journal entries
- ประเภท accruals มาตรฐาน
- ข้อกำหนด supporting documentation
- Review workflows และ approval controls

---

## ประเภท Accruals มาตรฐาน

### AP Accruals
บันทึกค่าใช้จ่ายที่เกิดขึ้นแล้วแต่ยังไม่ได้รับ invoice ณ วันปิดงวด
- Dr Expense / Cr Accrued Liabilities
- Reverse ในงวดถัดไปเมื่อได้รับ invoice จริง

### Prepaid Amortization
กระจาย prepaid expenses ตาม schedule
- Dr Expense / Cr Prepaid Asset
- ต้องมี amortization schedule เป็น supporting doc

### Fixed Asset Depreciation
บันทึก depreciation ตาม useful life ที่กำหนด
- Dr Depreciation Expense / Cr Accumulated Depreciation
- ใช้ fixed asset register เป็นฐาน

### Payroll Entries
บันทึก wages, taxes และ benefits ที่ค้างจ่าย
- Dr Payroll Expense / Cr Payroll Payable (และ Tax Payable)
- ต้องตรงกับ payroll register

### Revenue Recognition
บันทึก revenue ตาม ASC 606 / IFRS 15
- Dr Deferred Revenue / Cr Revenue (เมื่อ performance obligation completed)
- ต้องมี contract และ delivery evidence

---

## Supporting Documentation Requirements

| Entry Type | เอกสารที่ต้องมี |
|-----------|---------------|
| AP Accrual | Purchase order, service description, estimate basis |
| Prepaid | Payment invoice, amortization schedule |
| Depreciation | Fixed asset register, capitalization policy |
| Payroll | Payroll register, payroll approval |
| Revenue | Customer contract, delivery confirmation |
| Manual (อื่นๆ) | Business justification, calculation worksheet, approval email |

---

## Review Workflow

**Level 1 (Preparer)** — ตรวจสอบความถูกต้องของ debit/credit, account codes และ supporting docs ก่อน submit

**Level 2 (Supervisor)** — review และ approve entries ที่เกิน threshold (เช่น >$25K) ตรวจสอบ business rationale

**Level 3 (Controller)** — approve entries ที่มีนัยสำคัญสูง หรือ unusual entries

**Segregation of duties** — ผู้เตรียม ≠ ผู้ approve ≠ ผู้ post ใน ERP

---

## Common Errors ที่ต้องระวัง

**Period errors** — Post entry ในงวดผิด ตรวจสอบ transaction date และ posting date

**Account coding errors** — ใช้ account code ไม่ถูกต้อง ตรวจสอบ chart of accounts

**Cut-off errors** — Entry ของงวดนี้ถูก post ในงวดหน้า หรือกลับกัน

**Missing reversals** — Accrual entries ที่ไม่มี reversal ในงวดถัดไปทำให้ double-count
