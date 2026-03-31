# Skill Creator — ฉบับภาษาไทย

เอกสารนี้เป็นคำแปลภาษาไทยสำหรับผู้ใช้ที่ต้องการเข้าใจวิธีใช้และภาพรวมของ Skill Creator

---

## ภาพรวม

Skill Creator ช่วยให้คุณ **สร้าง**, **ปรับปรุง**, และ **วัดประสิทธิภาพ** ของ Skill สำหรับ Claude Code ตั้งแต่ต้นจนจบในที่เดียว

กระบวนการหลักมี 4 ขั้นตอน:
1. **Draft** — เขียน Skill ฉบับแรก
2. **Test** — รันทดสอบกับ prompt จริง
3. **Review** — ดูผลลัพธ์และให้ feedback
4. **Improve** — ปรับปรุงและวนซ้ำจนพอใจ

---

## วิธีเรียกใช้

พิมพ์ข้อความประเภทนี้เพื่อเรียก Skill Creator:

- "ช่วยสร้าง skill สำหรับ..."
- "อยากทำ skill ที่ทำให้ Claude..."
- "ปรับปรุง skill นี้ให้ดีขึ้น"
- "ทดสอบว่า skill ทำงานได้ถูกต้องไหม"
- "optimize description ของ skill นี้"

---

## โครงสร้างไฟล์ของ Skill

```
ชื่อ-skill/
├── SKILL.md              # ไฟล์หลัก (จำเป็น)
├── SKILL-TH.md           # คำแปลภาษาไทยสำหรับผู้ใช้อ่าน
├── scripts/              # สคริปต์ที่ใช้ซ้ำบ่อย
├── references/           # เอกสารอ้างอิงที่โหลดเมื่อต้องการ
└── assets/               # ไฟล์ที่ใช้ใน output
```

---

## กระบวนการสร้าง Skill ทีละขั้น

### ขั้นที่ 1 — กำหนดวัตถุประสงค์

Claude จะถามคำถามเหล่านี้เพื่อทำความเข้าใจความต้องการ:
- Skill นี้จะให้ Claude ทำอะไร?
- ควรทำงานเมื่อผู้ใช้พูดว่าอะไร?
- ผลลัพธ์ที่ต้องการอยู่ในรูปแบบใด?
- ต้องการ test case เพื่อตรวจสอบไหม?

### ขั้นที่ 2 — เขียน SKILL.md ฉบับแรก

Claude จะเขียน frontmatter และเนื้อหา Skill โดยองค์ประกอบสำคัญคือ:

| ส่วน | รายละเอียด |
|------|-----------|
| `name` | ตัวระบุ Skill (ใช้ suffix `-th` สำหรับ Localized skills) |
| `description` | เงื่อนไขการเรียกใช้ — ยิ่งชัดเจนยิ่งดี รวมวลีภาษาไทย |
| เนื้อหา | คำแนะนำ ขั้นตอน ตัวอย่าง และ reference |

### ขั้นที่ 3 — สร้างและรัน Test Cases

Claude จะสร้าง test prompt 2–3 ชุดที่สมจริง แล้วรันทั้งแบบ **มี Skill** และ **ไม่มี Skill** พร้อมกัน เพื่อเปรียบเทียบผลลัพธ์

### ขั้นที่ 4 — ดูผลและให้ Feedback

Claude จะเปิด **Eval Viewer** (HTML) ให้ดูผลลัพธ์แบบ side-by-side:
- แท็บ **Outputs** — เปรียบเทียบ output แต่ละ test case
- แท็บ **Benchmark** — สถิติเชิงปริมาณ (pass rate, เวลา, tokens)

เมื่อดูเสร็จ กด "Submit All Reviews" เพื่อส่ง feedback กลับมาให้ Claude ปรับปรุง

### ขั้นที่ 5 — ปรับปรุงและวนซ้ำ

Claude อ่าน feedback แล้วปรับ Skill ให้ดีขึ้น จากนั้นวนกลับไปขั้นที่ 3 จนกว่าจะพอใจ

---

## การ Optimize Description

Description ใน frontmatter คือกลไกหลักที่บอกให้ Claude รู้ว่าควรเรียก Skill เมื่อไหร่

Skill Creator มีระบบ Optimize Description อัตโนมัติ:
1. สร้าง eval query 20 ชุด (ควรและไม่ควร trigger)
2. ผู้ใช้ตรวจสอบและแก้ไข query ผ่าน HTML viewer
3. รัน optimization loop อัตโนมัติสูงสุด 5 รอบ
4. ได้ description ที่ดีที่สุดพร้อม score เปรียบเทียบ

---

## สคริปต์ที่มีใน Skill

| สคริปต์ | หน้าที่ |
|---------|--------|
| `scripts/run_eval.py` | รัน eval แต่ละชุด |
| `scripts/run_loop.py` | วน optimize description อัตโนมัติ |
| `scripts/aggregate_benchmark.py` | รวมผลและสร้าง benchmark.json |
| `scripts/generate_report.py` | สร้าง report |
| `scripts/improve_description.py` | ปรับปรุง description |
| `scripts/package_skill.py` | แพ็กเกจ Skill เป็น .skill file |
| `scripts/quick_validate.py` | ตรวจสอบ Skill เบื้องต้น |
| `eval-viewer/generate_review.py` | เปิด HTML viewer สำหรับ review |

---

## แนวปฏิบัติที่ดี

- ให้ description ชัดเจน รวมวลีภาษาไทยด้วยเสมอ
- เพิ่ม suffix `-th` ต่อท้ายชื่อ Skill ที่ Localize แล้ว
- อย่ารีบปรับ Skill ก่อนดูผลลัพธ์จาก Eval Viewer
- เก็บ script ที่ใช้ซ้ำบ่อยไว้ใน `scripts/` แทนการเขียนซ้ำทุกครั้ง
- รัน Description Optimization หลังจาก Skill อยู่ในสภาพที่พอใจแล้วเท่านั้น
