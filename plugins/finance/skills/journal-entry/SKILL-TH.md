# Skill: journal-entry — เตรียม Journal Entry

**ประเภท**: User-invoked — `/journal-entry <entry type> [period]`

เตรียม journal entries ที่ถูกต้องพร้อม debits, credits และรายละเอียดสนับสนุน สำหรับ month-end close และ audit documentation

> **ข้อสงวนสิทธิ์**: Plugin นี้ช่วยในงาน accounting workflow แต่ไม่ได้ให้คำแนะนำทางการเงิน ทุก output ควรได้รับการตรวจสอบโดยผู้เชี่ยวชาญก่อนนำไปใช้ใน financial reporting หรือ audit documentation

---

## วิธีเรียกใช้

```
/journal-entry ap-accrual 2025-03
/journal-entry prepaid 2025-Q1
/journal-entry fixed-assets March-2025
/journal-entry payroll 2025-03
/journal-entry revenue-recognition 2025-Q1
```

---

## ประเภท Entry ที่รองรับ

| Entry Type | คำอธิบาย | Accounts หลัก |
|-----------|---------|--------------|
| `ap-accrual` | AP accrual สำหรับค่าใช้จ่ายที่ยังไม่ได้รับ invoice | Expense Dr / Accrued Liabilities Cr |
| `prepaid` | Amortization ของ prepaid expenses | Expense Dr / Prepaid Asset Cr |
| `fixed-assets` | Depreciation ของ fixed assets | Depreciation Expense Dr / Accumulated Depreciation Cr |
| `payroll` | บันทึก payroll และ payroll taxes | Payroll Expense Dr / Payroll Liabilities Cr |
| `revenue-recognition` | Revenue recognition และ deferred revenue | Deferred Revenue Dr / Revenue Cr |
| `intercompany` | Intercompany eliminations | Intercompany Accounts |

---

## รูปแบบผลลัพธ์

```
## Journal Entry: [Entry Type] — [Period]

### Entry Header
| Field | Value |
|-------|-------|
| Date | [วันที่บันทึก] |
| Reference | JE-[YYYY-MM]-[XX] |
| Prepared By | [ชื่อ] |
| Approved By | [ชื่อ] |
| Description | [คำอธิบาย] |

### Debit/Credit Detail
| Account # | Account Name | Debit | Credit |
|-----------|-------------|-------|--------|
| [XXXX] | [ชื่อบัญชี] | $X | |
| [XXXX] | [ชื่อบัญชี] | | $X |
| | **Total** | **$X** | **$X** |

### Supporting Documentation
- [รายการเอกสารสนับสนุนที่ต้องแนบ]

### Review Notes
- [ประเด็นที่ควรตรวจสอบก่อน post]
```

---

## เคล็ดลับ

**Cut-off สำคัญ** — ตรวจสอบว่า entry อยู่ในงวดบัญชีที่ถูกต้อง โดยเฉพาะ entry ที่ทำใกล้สิ้นเดือน

**Supporting docs ครบถ้วน** — ทุก manual JE ควรมีเอกสารสนับสนุนที่เพียงพอสำหรับ audit (invoice, calculation worksheet, email approval)

**Segregation of duties** — ผู้เตรียม JE ไม่ควรเป็นผู้ approve และ post เอง

---

## การเชื่อมต่อที่ช่วยเพิ่มประสิทธิภาพ

เมื่อเชื่อมต่อ **~~erp** — ดึง account codes, GL balances และ post entries ได้โดยตรง

เมื่อเชื่อมต่อ **~~data warehouse** — ดึงข้อมูลประกอบสำหรับ accrual calculations
