# Skill: comp-analysis — วิเคราะห์ค่าตอบแทน

**ประเภท**: User-invoked — `/comp-analysis <role, level, หรือ dataset>`

วิเคราะห์ค่าตอบแทนสำหรับการ benchmark, จัดวาง band และวางแผน equity ช่วยเปรียบเทียบค่าตอบแทนกับตลาดสำหรับการจ้างงาน การรักษาพนักงาน และการวางแผน equity

---

## วิธีเรียกใช้

```
/comp-analysis Senior Software Engineer, SF
/comp-analysis อัปโหลดข้อมูล comp CSV เพื่อหา outlier
/comp-analysis model equity refresh grant 10K shares @ $50
```

---

## รูปแบบการวิเคราะห์

**Option A: วิเคราะห์ตำแหน่งเดียว** — ระบุ role, level และ location เพื่อรับ percentile benchmarks

**Option B: อัปโหลดข้อมูล comp** — อัปโหลด CSV หรือวาง comp bands เพื่อวิเคราะห์ band placement, หา outlier และเปรียบเทียบกับตลาด

**Option C: Model equity** — ระบุจำนวน shares, ราคาหุ้น และ vesting schedule เพื่อคำนวณ total comp

---

## องค์ประกอบค่าตอบแทน

| องค์ประกอบ | คำอธิบาย |
|-----------|---------|
| Base Salary | เงินเดือนฐาน |
| Equity | RSU, stock options หรือ equity อื่นๆ |
| Bonus | Annual bonus, signing bonus |
| Benefits | ประกันสุขภาพ, retirement, สวัสดิการอื่นๆ |

**ตัวแปรสำคัญ**: Role, Level, Location (SF vs. Austin vs. London ต่างกันมาก), Company stage, Industry

---

## ผลลัพธ์ที่ได้

ตาราง percentile (25th, 50th, 75th, 90th) สำหรับ base, equity และ total comp พร้อม location adjustment และ context ตาม company stage

```
## การวิเคราะห์ค่าตอบแทน: [Role/Scope]

### Benchmark ตลาด
| Percentile | Base | Equity | Total Comp |
|------------|------|--------|------------|
| 25th       | ...  | ...    | ...        |
| 50th       | ...  | ...    | ...        |
| 75th       | ...  | ...    | ...        |
| 90th       | ...  | ...    | ...        |

### การวิเคราะห์ Band (ถ้ามีข้อมูล)
| พนักงาน | Base ปัจจุบัน | Band Min | Band Mid | Band Max | ตำแหน่ง |
|---------|-------------|----------|----------|----------|---------|

### คำแนะนำ
- คำแนะนำค่าตอบแทน
- ประเด็น equity ที่ควรพิจารณา
- ความเสี่ยง retention (ถ้ามี)
```

---

## การเชื่อมต่อที่ช่วยเพิ่มประสิทธิภาพ

เมื่อเชื่อมต่อ **~~compensation data** — ดึง benchmark ตลาดที่ verified แบบ real-time ตาม role, level และ location

เมื่อเชื่อมต่อ **~~HRIS** — ดึงข้อมูล comp ปัจจุบันของพนักงานเพื่อวิเคราะห์ band placement และหา outlier อัตโนมัติ
