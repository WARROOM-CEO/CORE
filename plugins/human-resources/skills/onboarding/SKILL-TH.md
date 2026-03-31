# Skill: onboarding — แผน Onboarding พนักงานใหม่

**ประเภท**: User-invoked — `/onboarding <ชื่อพนักงานและตำแหน่ง>`

สร้างแผน onboarding ที่ครอบคลุมสำหรับพนักงานใหม่ ครอบคลุมตั้งแต่ pre-start tasks ไปถึงเป้าหมาย 90 วัน

---

## วิธีเรียกใช้

```
/onboarding Sarah Chen, Senior Product Manager
/onboarding John Smith, Software Engineer L4, เริ่ม 15 เมษายน
/onboarding ทีม Marketing มีพนักงานใหม่ 2 คนเดือนหน้า
```

---

## ข้อมูลที่ต้องการ

- **ชื่อพนักงาน**: ใครกำลังจะเริ่มงาน
- **Role**: ตำแหน่งงาน
- **ทีม**: เข้าร่วมทีมไหน
- **วันเริ่มงาน**: เริ่มเมื่อไหร่
- **Manager**: ใครเป็น manager

---

## โครงสร้างแผน Onboarding

### Pre-Start (ก่อน Day 1)
Tasks ที่ต้องทำก่อนพนักงานเริ่มงาน: ส่ง welcome email, ตั้งค่า accounts, สั่ง equipment, เพิ่มใน calendar meetings, กำหนด onboarding buddy

### Day 1
ตารางชั่วโมงต่อชั่วโมง — welcome & orientation, IT setup, แนะนำทีม, มื้อกลางวันต้อนรับ, role expectations

### Week 1
Compliance training, อ่าน documentation หลัก, 1:1 กับสมาชิกทีม, shadow meetings, งานชิ้นแรก, check-in กับ manager

### เป้าหมาย 30/60/90 วัน
เป้าหมายที่วัดผลได้ 3 ระยะ ออกแบบตาม role และความคาดหวัง

---

## ผลลัพธ์ที่ได้

```
## แผน Onboarding: [ชื่อ] — [Role]
วันเริ่มงาน: [วันที่] | ทีม: [ทีม] | Manager: [Manager]

### Pre-Start          ### Day 1 (ตารางชั่วโมง)
### Week 1            ### เป้าหมาย 30/60/90 วัน
### ผู้ติดต่อหลัก      ### รายการ Tools ที่ต้องขอ access
```

---

## เคล็ดลับ

**ปรับตาม role** — onboarding ของ engineer ต่างจาก designer กำหนด tools และ documentation ตาม role จริง

**อย่าโหลด Day 1 มากเกินไป** — เน้น setup และความสัมพันธ์ งานจริงเริ่ม Week 2

**กำหนด buddy เสมอ** — การมีคนที่ไม่ใช่ manager ให้ถามทำให้ประสบการณ์ onboarding ดีขึ้นอย่างมีนัยสำคัญ

---

## การเชื่อมต่อที่ช่วยเพิ่มประสิทธิภาพ

เมื่อเชื่อมต่อ **~~HRIS** — ดึงข้อมูลพนักงานและ org chart, auto-populate รายการ tools ตาม role

เมื่อเชื่อมต่อ **~~knowledge base** — เชื่อมโยงไปยัง onboarding docs, team wikis และ runbooks ที่เกี่ยวข้อง

เมื่อเชื่อมต่อ **~~calendar** — สร้าง calendar events Day 1 และ meeting invites Week 1 อัตโนมัติ
