# Skill: people-report — รายงาน People Analytics

**ประเภท**: User-invoked — `/people-report <ประเภทรายงาน — headcount, attrition, diversity, org health>`

สร้างรายงาน people analytics จากข้อมูล HR วิเคราะห์ workforce data เพื่อหา trends, risks และโอกาสพัฒนา

---

## วิธีเรียกใช้

```
/people-report headcount
/people-report attrition Q1 2026
/people-report diversity ระดับ Senior และสูงกว่า
/people-report org health ทีม Engineering
```

---

## ประเภทรายงาน

**Headcount** — Snapshot org ปัจจุบัน จำแนกตามทีม, location, level, tenure

**Attrition** — วิเคราะห์ turnover แยก voluntary/involuntary, ตามทีม, แนวโน้มเวลา

**Diversity** — ตัวชี้วัด representation ตาม level, ทีม, pipeline

**Org Health** — Span of control, management layers, ขนาดทีม, flight risk

---

## ตัวชี้วัดหลัก

### Retention
- อัตรา attrition รวม (voluntary + involuntary)
- Regrettable attrition rate
- Average tenure
- Flight risk indicators

### Diversity
- Representation ตาม level, ทีม และ function
- Pipeline diversity (hiring funnel แยก demographic)
- อัตรา promotion ตามกลุ่ม
- Pay equity analysis

### Engagement
- Survey scores และแนวโน้ม
- eNPS (Employee Net Promoter Score)
- Participation rates

### Productivity
- Revenue per employee
- Span of control efficiency
- Time to productivity สำหรับพนักงานใหม่

---

## ข้อมูลที่ต้องการ

อัปโหลด CSV หรืออธิบายข้อมูล ฟิลด์ที่มีประโยชน์:
- Employee name/ID, department, team
- Title, level, location
- Start date, end date (ถ้ามี)
- Manager, compensation (ถ้าเกี่ยวข้อง)
- Demographics (สำหรับ diversity reports ถ้ามี)

---

## รูปแบบรายงาน

```
## รายงาน People: [ประเภท] — [วันที่]

### Executive Summary
[2-3 ประเด็นสำคัญ]

### ตัวชี้วัดหลัก
| Metric | Value | Trend |
|--------|-------|-------|

### การวิเคราะห์เชิงลึก
[ตาราง กราฟ และคำอธิบายตามประเภทรายงาน]

### คำแนะนำ
[คำแนะนำที่มาจากข้อมูล + action items]

### Methodology
[วิธีคำนวณและข้อจำกัดของข้อมูล]
```

---

## การเชื่อมต่อที่ช่วยเพิ่มประสิทธิภาพ

เมื่อเชื่อมต่อ **~~HRIS** — ดึงข้อมูลพนักงานแบบ live โดยไม่ต้องอัปโหลด CSV

เมื่อเชื่อมต่อ **~~chat** — แชร์สรุปรายงานใน channel ที่เกี่ยวข้องได้ทันที
