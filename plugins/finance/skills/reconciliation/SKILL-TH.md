# Skill: reconciliation — กระทบยอดบัญชี

**ประเภท**: User-invoked — `/reconciliation <account> [period]`

กระทบยอดบัญชีโดยเปรียบเทียบ GL balances กับ subledgers, bank statements หรือข้อมูลจากภายนอก ระบุและจำแนก reconciling items

> **ข้อสงวนสิทธิ์**: Plugin นี้ช่วยในงาน reconciliation workflow แต่ไม่ได้ให้คำแนะนำทางการเงิน ทุก output ควรได้รับการตรวจสอบโดยผู้เชี่ยวชาญก่อนนำไปใช้ใน financial reporting

---

## วิธีเรียกใช้

```
/reconciliation cash 2025-03
/reconciliation accounts-receivable 2025-Q1
/reconciliation accounts-payable March-2025
/reconciliation intercompany 2025-03
```

---

## ประเภท Reconciliation ที่รองรับ

**Bank Reconciliation** — เปรียบเทียบ GL cash balance กับ bank statement ระบุ outstanding checks, deposits in transit และ bank errors

**GL-to-Subledger Reconciliation** — เปรียบเทียบ GL control account กับ subledger totals (AR, AP, Fixed Assets, Inventory)

**Intercompany Reconciliation** — ตรวจสอบว่า intercompany balances ตรงกันระหว่าง entities และ eliminate ก่อน consolidation

**Third-Party Reconciliation** — เปรียบเทียบกับข้อมูลจากภายนอก เช่น processor statements, custodian reports

---

## รูปแบบผลลัพธ์

```
## Reconciliation: [Account] — [Period]

### Summary
| | Amount |
|--|--------|
| GL Balance | $X |
| External Balance (Bank/Subledger) | $X |
| **Unexplained Difference** | **$X** |

### Reconciling Items
| # | Description | Type | Amount | Age | Status |
|---|------------|------|--------|-----|--------|
| 1 | [รายการ] | [Outstanding Check / Deposit in Transit / Error / Other] | $X | [X วัน] | [Open/Resolved] |

### Aging Summary
| อายุ | จำนวนรายการ | มูลค่า |
|------|------------|-------|
| 0-30 วัน | | |
| 31-60 วัน | | |
| 60+ วัน | | |

### Required Actions
- [Action items สำหรับรายการที่ค้างอยู่]
```

---

## สัญญาณเตือนที่ควรระวัง

**Reconciling items อายุมาก** — รายการที่ค้างมากกว่า 30 วันควรได้รับการตรวจสอบ รายการที่ค้างมากกว่า 90 วันต้องมีเหตุผลชัดเจน

**Offsetting items** — ระวัง items ที่ถูก net กันเพื่อซ่อน errors

**Recurring items** — รายการเดิมที่ปรากฏทุกเดือนอาจเป็นสัญญาณของ systematic error

---

## การเชื่อมต่อที่ช่วยเพิ่มประสิทธิภาพ

เมื่อเชื่อมต่อ **~~erp** — ดึง GL balances และ subledger data อัตโนมัติ

เมื่อเชื่อมต่อ **~~data warehouse** — query ข้อมูลประวัติเพื่อ trend analysis และ pattern detection
