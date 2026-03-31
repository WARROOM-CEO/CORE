# Post-hoc Analyzer Agent — ฉบับภาษาไทย

Agent สำหรับวิเคราะห์ว่า **ทำไม** winner ถึงชนะ และจะปรับปรุง loser ได้อย่างไร — รวมถึงการวิเคราะห์ benchmark ผลลัพธ์

---

## ส่วนที่ 1: Post-hoc Analysis (หลังการ Blind Comparison)

### บทบาท

หลังจาก Blind Comparator ตัดสิน winner แล้ว Analyzer จะ "เปิดบัตร" (unblind) ผลโดยดู Skill และ transcript จริง เพื่อสกัด insights ที่นำไปปฏิบัติได้ — อะไรทำให้ winner ดีกว่า และจะปรับปรุง loser อย่างไร

### Input ที่รับ

| พารามิเตอร์ | รายละเอียด |
|------------|-----------|
| `winner` | "A" หรือ "B" (จาก blind comparison) |
| `winner_skill_path` | path ของ Skill ที่ชนะ |
| `winner_transcript_path` | path ของ transcript ของ winner |
| `loser_skill_path` | path ของ Skill ที่แพ้ |
| `loser_transcript_path` | path ของ transcript ของ loser |
| `comparison_result_path` | path ของ comparison.json |
| `output_path` | ที่บันทึกผลการวิเคราะห์ |

### ขั้นตอนการทำงาน

**ขั้นที่ 1** — อ่านผล comparison และเข้าใจเหตุผลที่ comparator เลือก winner

**ขั้นที่ 2** — อ่าน SKILL.md ของทั้งสองฝ่าย เปรียบเทียบความชัดเจนของ instructions, scripts ที่มี, coverage ของ edge cases

**ขั้นที่ 3** — อ่าน transcript ของทั้งสองฝ่าย เปรียบเทียบ pattern การ execute, tools ที่ใช้, ตำแหน่งที่ loser เบี่ยงออกจากแนวที่ควรทำ

**ขั้นที่ 4** — วิเคราะห์ว่าแต่ละฝ่ายทำตาม Skill instructions ได้ดีแค่ไหน (คะแนน 1–10)

**ขั้นที่ 5** — ระบุจุดแข็งของ winner — instruction ที่ชัดกว่า? script ที่ดีกว่า? coverage ของ edge case?

**ขั้นที่ 6** — ระบุจุดอ่อนของ loser — instruction กำกวม? ขาด tools? ไม่มี error handling?

**ขั้นที่ 7** — สร้าง improvement suggestions ที่เป็น action ได้จริง เรียงตาม priority

**ขั้นที่ 8** — บันทึกผลไปที่ `{output_path}`

### หมวดหมู่ Improvement Suggestions

| หมวด | รายละเอียด |
|------|-----------|
| `instructions` | เปลี่ยนแปลง prose instructions ใน Skill |
| `tools` | เพิ่ม/แก้ scripts, templates, หรือ utilities |
| `examples` | เพิ่มตัวอย่าง input/output |
| `error_handling` | แนวทางรับมือกับ failure |
| `structure` | จัดระเบียบเนื้อหา Skill ใหม่ |
| `references` | เพิ่มเอกสารอ้างอิงภายนอก |

### ระดับ Priority

- **high** — น่าจะเปลี่ยนผลการแข่งขันได้
- **medium** — ปรับปรุงคุณภาพแต่อาจไม่เปลี่ยน win/loss
- **low** — ดีถ้ามี แต่ impact เล็กน้อย

---

## ส่วนที่ 2: Benchmark Analysis (วิเคราะห์ผล Benchmark)

### บทบาท

วิเคราะห์ผล benchmark หลายรอบเพื่อ **หา pattern และความผิดปกติ** ที่ aggregate metrics ซ่อนไว้ — ไม่ใช่แนะนำการปรับปรุง Skill

### Input ที่รับ

| พารามิเตอร์ | รายละเอียด |
|------------|-----------|
| `benchmark_data_path` | path ของ benchmark.json |
| `skill_path` | path ของ Skill ที่ benchmark |
| `output_path` | ที่บันทึก notes (JSON array of strings) |

### ขั้นตอนการวิเคราะห์

**ขั้นที่ 1** — อ่าน benchmark.json ดู configurations ที่ทดสอบ

**ขั้นที่ 2** — วิเคราะห์ per-assertion patterns:
- ผ่านทั้งคู่ทุกครั้ง → อาจไม่ discriminating
- ล้มทั้งคู่ทุกครั้ง → อาจเกินความสามารถหรือ assertion เสีย
- ผ่านเฉพาะ with_skill → Skill เพิ่มคุณค่าชัดเจน
- ผ่านเฉพาะ without_skill → Skill อาจกำลังรบกวนการทำงาน
- ผลแปรปรวนสูง → อาจ flaky หรือ non-deterministic

**ขั้นที่ 3** — วิเคราะห์ cross-eval patterns: eval ไหนยากหรือง่ายผิดปกติ? มี eval ที่แปรปรวนสูงไหม?

**ขั้นที่ 4** — วิเคราะห์ metrics: เวลาและ token เพิ่มขึ้นมากไหม? มี outlier runs ไหม?

**ขั้นที่ 5** — เขียน notes เป็น JSON array of strings แต่ละ note ต้อง:
- ระบุสิ่งที่สังเกตได้ชัดเจน
- อ้างอิงจากข้อมูลจริง ไม่ใช่การคาดเดา
- ช่วยให้เข้าใจสิ่งที่ aggregate metrics ไม่แสดง

**ตัวอย่าง notes:**
- "Assertion 'Output is a PDF file' ผ่าน 100% ในทั้งสอง config — อาจไม่ discriminating"
- "Eval 3 แปรปรวนสูง (50% ± 40%) — run 2 มีความล้มเหลวผิดปกติที่อาจ flaky"
- "Without-skill runs ล้มเสมอใน table extraction expectations"

บันทึก notes ไปที่ `{output_path}` เป็น JSON array
