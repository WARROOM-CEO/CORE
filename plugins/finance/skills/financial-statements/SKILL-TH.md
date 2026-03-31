# Skill: financial-statements — สร้าง Financial Statements

**ประเภท**: User-invoked — `/financial-statements <frequency> <period>`

สร้าง financial statements พร้อม period-over-period comparison และ variance analysis ตามมาตรฐาน GAAP

> **ข้อสงวนสิทธิ์**: Plugin นี้ช่วยในงาน financial reporting workflow แต่ไม่ได้ให้คำแนะนำทางการเงิน ทุก output ควรได้รับการตรวจสอบโดยผู้เชี่ยวชาญก่อนนำไปใช้ใน regulatory filings หรือ external reporting

---

## วิธีเรียกใช้

```
/financial-statements monthly 2025-03
/financial-statements quarterly 2025-Q1
/financial-statements ytd March-2025
/financial-statements monthly 2025-03 vs budget
```

---

## งบการเงินที่รองรับ

**Income Statement (P&L)** — Revenue, COGS, Gross Profit, Operating Expenses, EBITDA, Net Income พร้อม variance vs. prior period และ budget

**Balance Sheet** — Assets, Liabilities, Equity ณ วันปิดงวด พร้อม period-over-period changes

**Cash Flow Statement** — Operating, Investing, Financing activities แบบ indirect method

---

## รูปแบบผลลัพธ์

```
## [ชื่องบ]: [Period]

| Line Item | Actual | Prior Period | Variance $ | Variance % | Budget | Budget Var % |
|-----------|--------|-------------|------------|------------|--------|-------------|
| Revenue | $X | $X | $X | X% | $X | X% |
| COGS | ($X) | ($X) | $X | X% | ($X) | X% |
| **Gross Profit** | **$X** | **$X** | | **X%** | | |
| Operating Expenses | ($X) | ($X) | | | | |
| **EBITDA** | **$X** | **$X** | | **X%** | | |
| **Net Income** | **$X** | **$X** | | **X%** | | |

### Material Variances (>X% หรือ >$X)
| Line Item | Variance | คำอธิบาย |
|-----------|---------|---------|
| [บัญชี] | $X (X%) | [สาเหตุ] |

### GAAP Notes
[ข้อสังเกต GAAP presentation ที่เกี่ยวข้อง]
```

---

## ค่า Threshold ที่ใช้ Flag Variances

Variances ที่มีนัยสำคัญและต้องอธิบาย:
- มากกว่า **5%** ของ line item
- มากกว่า **$50,000** (ปรับได้ตามขนาดองค์กร)
- ทุก line item ที่ขยับจาก positive เป็น negative หรือกลับกัน

---

## การเชื่อมต่อที่ช่วยเพิ่มประสิทธิภาพ

เมื่อเชื่อมต่อ **~~erp** — ดึง trial balance และ GL data อัตโนมัติ ไม่ต้องอัปโหลด

เมื่อเชื่อมต่อ **~~data warehouse** — query ข้อมูลประวัติสำหรับ multi-period comparison

เมื่อเชื่อมต่อ **~~analytics** — ดึง KPI dashboards เพื่อประกอบการอธิบาย variances
