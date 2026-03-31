# Skill: variance-analysis — วิเคราะห์ Variance

**ประเภท**: User-invoked — `/variance-analysis <line item> <period> vs <comparison>`

แยกวิเคราะห์ financial variances ตาม drivers พร้อมคำอธิบาย narrative และ waterfall analysis สำหรับ management reporting

> **ข้อสงวนสิทธิ์**: Plugin นี้ช่วยในงาน variance analysis workflow แต่ไม่ได้ให้คำแนะนำทางการเงิน ทุก output ควรได้รับการตรวจสอบโดยผู้เชี่ยวชาญ

---

## วิธีเรียกใช้

```
/variance-analysis revenue 2025-Q1 vs 2024-Q1
/variance-analysis opex 2025-03 vs budget
/variance-analysis gross-margin 2025-Q1 vs 2024-Q4
/variance-analysis headcount-cost March-2025 vs February-2025
```

---

## เทคนิคการแยกวิเคราะห์

**Price/Volume Analysis** — แยก variance ออกเป็นส่วนที่เกิดจากราคา (rate) และส่วนที่เกิดจากปริมาณ (volume)

**Rate/Mix Analysis** — วิเคราะห์ว่า variance เกิดจาก rate ที่เปลี่ยนไป หรือ mix ของสินค้า/บริการที่เปลี่ยนไป

**Bridge Analysis** — แสดง path จากตัวเลข starting point ไปยัง ending point ผ่าน drivers แต่ละตัว

---

## รูปแบบผลลัพธ์

```
## Variance Analysis: [Line Item]
Period: [Current] vs [Comparison] | Total Variance: $X (X%)

### Waterfall: Driver Breakdown
Starting Point ([Comparison]): $X
+ [Driver 1]: +$X (X%)   → [คำอธิบาย]
+ [Driver 2]: +$X (X%)   → [คำอธิบาย]
- [Driver 3]: -$X (X%)   → [คำอธิบาย]
Ending Point ([Current]): $X

### Driver Detail
| Driver | Impact $ | Impact % | คำอธิบาย | Action Required |
|--------|---------|---------|---------|----------------|
| [Volume] | $X | X% | [สาเหตุ] | [Y/N] |
| [Price/Rate] | $X | X% | [สาเหตุ] | [Y/N] |
| [Mix] | $X | X% | [สาเหตุ] | [Y/N] |
| [Other] | $X | X% | [สาเหตุ] | [Y/N] |

### Narrative Summary
[คำอธิบาย 2-3 ประโยคสำหรับผู้บริหาร — ไม่มี jargon]

### Recommended Actions
- [Action item ที่ต้องดำเนินการ]
```

---

## ระดับ Materiality

| ระดับ | Threshold | การดำเนินการ |
|------|----------|------------|
| Material | >5% และ >$100K | อธิบายอย่างละเอียด + action plan |
| Notable | 2-5% หรือ $25K-$100K | อธิบายสั้น |
| Immaterial | <2% และ <$25K | บันทึกไว้เฉยๆ ไม่ต้องอธิบาย |

*ปรับ threshold ตามขนาดและบริบทขององค์กร*

---

## การเชื่อมต่อที่ช่วยเพิ่มประสิทธิภาพ

เมื่อเชื่อมต่อ **~~data warehouse** — query ข้อมูลประวัติและ driver data อัตโนมัติ

เมื่อเชื่อมต่อ **~~analytics** — ดึง KPI trends และ segment data เพื่ออธิบาย drivers ได้แม่นยำยิ่งขึ้น

เมื่อเชื่อมต่อ **~~erp** — ดึง actuals และ budget data แบบ real-time
