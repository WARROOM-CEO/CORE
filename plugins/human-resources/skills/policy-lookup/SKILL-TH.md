# Skill: policy-lookup — ค้นหา Company Policy

**ประเภท**: User-invoked — `/policy-lookup <หัวข้อ policy — PTO, สวัสดิการ, travel, ค่าใช้จ่าย ฯลฯ>`

ค้นหาและอธิบาย company policy ด้วยภาษาที่เข้าใจง่าย ตอบคำถามของพนักงานเกี่ยวกับ policies, สวัสดิการ และขั้นตอนต่างๆ

---

## วิธีเรียกใช้

```
/policy-lookup นโยบาย PTO
/policy-lookup ทำงานจากต่างประเทศได้ไหม
/policy-lookup ค่าใช้จ่ายรายงานอย่างไร
/policy-lookup สวัสดิการ parental leave
```

---

## หัวข้อ Policy ทั่วไป

| หมวด | ตัวอย่างคำถาม |
|------|-------------|
| PTO และการลา | วันลาพักร้อน, ลาป่วย, parental leave, bereavement, sabbatical |
| สวัสดิการ | ประกันสุขภาพ, ทันตกรรม, สายตา, 401k, HSA/FSA, wellness |
| ค่าตอบแทน | รอบจ่ายเงินเดือน, bonus timing, equity vesting, reimbursement |
| Remote Work | WFH policy, remote locations, equipment stipend, coworking |
| Travel | วิธีจองตั๋ว, per diem, expense report, ขั้นตอนอนุมัติ |
| Code of Conduct | กฎจรรยาบรรณ, นโยบาย harassment, conflicts of interest |
| การพัฒนาตัวเอง | งบ training, conference policy, tuition reimbursement |

---

## วิธีการตอบคำถาม

1. ค้นหา `~~knowledge base` เพื่อหา policy document ที่เกี่ยวข้อง
2. ให้คำตอบที่ชัดเจนด้วยภาษาที่เข้าใจง่าย
3. อ้างอิงข้อความ policy จริง
4. ระบุข้อยกเว้นหรือกรณีพิเศษ
5. บอกว่าควรติดต่อใครสำหรับ edge cases

**guardrails สำคัญ**: อ้างอิง source document เสมอ — ถ้าไม่พบ policy ให้บอกตรงๆ ไม่ใช่เดา สำหรับคำถาม compliance หรือ legal ให้แนะนำปรึกษา HR หรือ legal โดยตรง

---

## รูปแบบผลลัพธ์

```
## Policy: [หัวข้อ]

### คำตอบสั้น
[1-2 ประโยค ตอบตรงๆ]

### รายละเอียด
[รายละเอียด policy อธิบายด้วยภาษาเข้าใจง่าย]

### ข้อยกเว้น / กรณีพิเศษ
[ข้อยกเว้นที่เกี่ยวข้อง]

### ผู้ที่ควรติดต่อ
[บุคคลหรือทีมสำหรับคำถามนอกเหนือจากที่เอกสารระบุ]

### Source
[ชื่อเอกสาร, หน้า หรือส่วนที่มาของข้อมูล]
```

---

## เคล็ดลับ

**ถามแบบธรรมชาติ** — "ทำงานจากยุโรปได้ไหมหนึ่งเดือน" ดีกว่า "international remote work policy"

**ยิ่งเจาะจงยิ่งดี** — "PTO สำหรับพนักงาน part-time ใน California" ได้คำตอบดีกว่า "PTO policy"

---

## การเชื่อมต่อที่ช่วยเพิ่มประสิทธิภาพ

เมื่อเชื่อมต่อ **~~knowledge base** — ค้นหา employee handbook และ policy documents อัตโนมัติ พร้อมอ้างอิงเอกสาร, หน้า และส่วนที่เจาะจง

เมื่อเชื่อมต่อ **~~HRIS** — ดึงข้อมูลเฉพาะพนักงาน เช่น PTO balance, benefits elections และสถานะ enrollment
