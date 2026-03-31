# Skill: draft-offer — ร่าง Offer Letter

**ประเภท**: User-invoked — `/draft-offer <role and level>`

ร่าง offer letter ที่สมบูรณ์พร้อมรายละเอียดค่าตอบแทน วันเริ่มงาน และเงื่อนไขการจ้างงาน

---

## วิธีเรียกใช้

```
/draft-offer Senior Engineer, L5
/draft-offer Head of Marketing
/draft-offer Product Manager, mid-level, remote
```

---

## ข้อมูลที่ต้องการ

- **Role และ Title**: ตำแหน่งงานคืออะไร
- **Level**: Junior, Mid, Senior, Staff ฯลฯ
- **Location**: พนักงานจะทำงานที่ไหน (กระทบ comp และสวัสดิการ)
- **ค่าตอบแทน**: Base salary, equity, signing bonus (ถ้ามี)
- **วันเริ่มงาน**: เริ่มเมื่อไหร่
- **Hiring Manager**: รายงานตรงต่อใคร

หากข้อมูลไม่ครบ จะช่วยให้คิดและกรอกข้อมูลที่ขาด

---

## ผลลัพธ์ที่ได้

```
## ร่าง Offer Letter: [Role] — [Level]

### แพ็กเกจค่าตอบแทน
| องค์ประกอบ | รายละเอียด |
|-----------|-----------|
| Base Salary | $X/ปี |
| Equity | X shares/units, vesting schedule |
| Signing Bonus | $X (ถ้ามี) |
| Target Bonus | X% ของ base (ถ้ามี) |
| Total Comp ปีแรก | $X |

### เงื่อนไข
- วันเริ่มงาน: [วันที่]
- รายงานตรงต่อ: [Manager]
- Location: Office / Remote / Hybrid
- ประเภทการจ้าง: Full-time

### สรุปสวัสดิการ
[สวัสดิการหลักที่เกี่ยวข้องกับ candidate]

### ข้อความ Offer Letter
[ข้อความ offer letter ฉบับสมบูรณ์]

### หมายเหตุสำหรับ Hiring Manager
- Guidance การเจรจา (ถ้าจำเป็น)
- Context ของ comp band
- ข้อสังเกตหรือประเด็นที่ควรระวัง
```

---

## เคล็ดลับ

**Total comp สำคัญกว่า base** — candidate เปรียบเทียบ total compensation ไม่ใช่แค่เงินเดือน ควรระบุ equity, bonus และสวัสดิการให้ชัดเจน

**ระบุ equity อย่างละเอียด** — จำนวน shares, วิธีประเมินมูลค่าปัจจุบัน, vesting schedule ทำให้ candidate เข้าใจมูลค่าจริง

**ปรับให้เป็นส่วนตัว** — อ้างอิงบางสิ่งจากกระบวนการสัมภาษณ์เพื่อให้รู้สึกอบอุ่น

---

## การเชื่อมต่อที่ช่วยเพิ่มประสิทธิภาพ

เมื่อเชื่อมต่อ **~~HRIS** — ดึงข้อมูล comp band, ตรวจสอบการอนุมัติ headcount และ auto-populate ข้อมูลสวัสดิการ

เมื่อเชื่อมต่อ **~~ATS** — ดึงข้อมูล candidate จาก application และอัปเดตสถานะ offer ใน pipeline
