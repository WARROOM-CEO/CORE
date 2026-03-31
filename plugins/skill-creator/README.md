# skill-creator — Thai Edition

**ปลั๊กอินสำหรับสร้าง ปรับปรุง และวัดประสิทธิภาพ Skill ของ Claude Code — Claude สื่อสารเป็นภาษาไทยตลอดการใช้งาน**

---

## ภาพรวมการทำงาน

Skill Creator นำผู้ใช้ผ่านวงจรการพัฒนา Skill แบบครบวงจร ตั้งแต่ไอเดียเริ่มต้นจนถึง Skill ที่ผ่านการทดสอบและพร้อมใช้งาน:

```
Draft → Test (with/without skill, parallel) → Review ผ่าน HTML Viewer
→ Improve → วนซ้ำจนพอใจ → Optimize Description → Package
```

Claude จะ **ระบุตำแหน่งในวงจร** ให้อัตโนมัติ เช่น ถ้าผู้ใช้มี draft Skill อยู่แล้ว จะข้ามไปขั้น eval ได้ทันที หรือถ้าต้องการแค่ optimize description ก็รันเฉพาะส่วนนั้น

---

## Skills ทั้งหมด

### `skill-creator-th` — Model-invoked

**หน้าที่:** ดูแลกระบวนการสร้างและปรับปรุง Skill ทั้งหมด ตั้งแต่ต้นจนถึง Package

**เรียกใช้เมื่อ:** ผู้ใช้พูดถึง "สร้าง skill ใหม่", "ปรับปรุง skill", "ทดสอบ skill", "วัดประสิทธิภาพ skill", "optimize description ของ skill", "create a skill", "improve this skill", "run evals"

**กระบวนการหลัก:**

| ขั้นตอน | รายละเอียด | เครื่องมือที่ใช้ |
|---------|-----------|----------------|
| 1. Capture Intent | สัมภาษณ์ความต้องการ, trigger, output format | สนทนา / AskUserQuestion |
| 2. Write SKILL.md | เขียน frontmatter + เนื้อหาตามที่ออกแบบ | Write / Edit |
| 3. Create Test Cases | สร้าง eval prompts 2–3 ชุด บันทึกใน evals.json | Write |
| 4. Run Evals (Parallel) | spawn subagents: with_skill + baseline พร้อมกัน | Agent (parallel) |
| 5. Grade & Benchmark | ประเมิน assertions, รวมสถิติ, วิเคราะห์ pattern | scripts/ |
| 6. Launch Viewer | สร้าง HTML reviewer ให้ผู้ใช้ดู output และให้ feedback | eval-viewer/ |
| 7. Improve | อ่าน feedback.json แล้วปรับปรุง Skill | Edit |
| 8. Repeat | วนซ้ำขั้น 4–7 จนผู้ใช้พอใจ | — |
| 9. Optimize Description | รัน run_loop.py เพื่อหา description ที่ trigger แม่นที่สุด | scripts/ |
| 10. Package | สร้าง .skill file ส่งให้ผู้ใช้ | scripts/package_skill.py |

Plugin นี้มี **Skill เดียว** ที่ครอบคลุมทุกกรณี — สร้างใหม่, ปรับปรุง, ทดสอบ, และ optimize

---

## โครงสร้างไฟล์ (Bilingual Design)

```
skill-creator/
├── .claude-plugin/
│   └── plugin.json                        # metadata: ชื่อ, author WARROOM-CEO
├── skills/
│   └── skill-creator/                     # Skill เดียวที่ครอบคลุมทุกกรณี
│       ├── SKILL.md                       # คำสั่ง Claude (EN + ไทยส่วนสื่อกับผู้ใช้)
│       ├── SKILL-TH.md                    # คำแปลไทยสำหรับผู้ใช้อ่าน
│       ├── agents/
│       │   ├── grader.md                  # คำสั่ง Grader subagent: ตรวจให้คะแนน assertions (EN)
│       │   ├── grader-TH.md               # คำแปลภาษาไทย
│       │   ├── comparator.md              # คำสั่ง Blind Comparator: เปรียบเทียบ output สองชิ้น (EN)
│       │   ├── comparator-TH.md           # คำแปลภาษาไทย
│       │   ├── analyzer.md                # คำสั่ง Post-hoc Analyzer + Benchmark Analyzer (EN)
│       │   └── analyzer-TH.md             # คำแปลภาษาไทย
│       ├── references/
│       │   ├── schemas.md                 # JSON schemas ทั้งหมด (evals, grading, benchmark ฯลฯ) (EN)
│       │   └── schemas-TH.md             # คำแปลภาษาไทย
│       ├── scripts/
│       │   ├── run_eval.py                # รัน eval แต่ละชุด
│       │   ├── run_loop.py                # วน optimize description อัตโนมัติสูงสุด 5 รอบ
│       │   ├── aggregate_benchmark.py     # รวมผลทุก run สร้าง benchmark.json + benchmark.md
│       │   ├── generate_report.py         # สร้าง report สรุป
│       │   ├── improve_description.py     # ปรับปรุง description ด้วย extended thinking
│       │   ├── package_skill.py           # แพ็กเกจ Skill เป็น .skill file
│       │   ├── quick_validate.py          # ตรวจสอบ SKILL.md เบื้องต้น
│       │   └── utils.py                   # utilities ร่วม
│       ├── assets/
│       │   └── eval_review.html           # HTML template สำหรับ Description Optimization eval review
│       ├── eval-viewer/
│       │   ├── generate_review.py         # สร้างและเปิด HTML viewer สำหรับ review output
│       │   └── viewer.html                # Template หน้า reviewer (Outputs tab + Benchmark tab)
│       └── LICENSE.txt                    # License ของ Skill นี้
├── LICENSE                                # Apache 2.0 ฉบับเต็ม (EN)
└── README.md                              # เอกสารนี้ (ไทย)
```

| ไฟล์/Folder | ภาษา | ใช้โดย | วัตถุประสงค์ |
|-------------|------|--------|--------------|
| `skills/*/SKILL.md` | EN + ไทย (ส่วนสื่อผู้ใช้) | Claude | คำสั่งหลัก ประหยัด Token |
| `skills/*/SKILL-TH.md` | ไทยทั้งหมด | ผู้ใช้ | อ่านทำความเข้าใจ Skill |
| `agents/*.md` | อังกฤษ | Claude (subagent) | คำสั่ง subagent เฉพาะทาง |
| `agents/*-TH.md` | ไทยทั้งหมด | ผู้ใช้ | คำแปล subagent instructions |
| `references/*.md` | อังกฤษ | Claude | JSON schemas, โหลดเมื่อต้องการ |
| `references/*-TH.md` | ไทยทั้งหมด | ผู้ใช้ | คำแปลเอกสารอ้างอิง |
| `scripts/*.py` | Python | Claude (Bash) | งานคำนวณและ automation ซ้ำๆ |
| `assets/eval_review.html` | HTML/JS | Claude | Template สำหรับ eval query review |
| `eval-viewer/` | Python + HTML | Claude | เปิด reviewer ให้ผู้ใช้ดู output |

---

## สัญญาอนุญาต (License)

### งานต้นฉบับ

ปลั๊กอินนี้ดัดแปลงมาจาก **skill-creator** โดย Anthropic, PBC ซึ่งเผยแพร่ภายใต้ **Apache License, Version 2.0**

```
Copyright Anthropic, PBC

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0
```

### งานดัดแปลง (Derivative Work)

**skill-creator (Thai Edition)** เป็นงานดัดแปลง (Derivative Work) ตามนิยามของ Apache License 2.0 โดย **WARROOM-CEO** มีการเปลี่ยนแปลงดังนี้:

- แก้ไข `skills/skill-creator/SKILL.md`: เพิ่ม Thai Language Instruction Block, เปลี่ยนชื่อ skill เป็น `skill-creator-th`, เพิ่ม trigger phrases ภาษาไทย
- เพิ่ม `skills/skill-creator/SKILL-TH.md`: คำแปลภาษาไทยเต็มรูปแบบอธิบายกระบวนการทำงาน
- เพิ่ม `agents/grader-TH.md`, `agents/comparator-TH.md`, `agents/analyzer-TH.md`: คำแปลภาษาไทยของคำสั่ง subagent ทั้งหมด
- เพิ่ม `references/schemas-TH.md`: คำแปลภาษาไทยของ JSON schemas ทั้งหมด
- เขียนใหม่ `README.md` เป็นภาษาไทย ตามมาตรฐาน Bilingual Design Pattern
- แก้ไข `plugin.json`: เปลี่ยน author จาก Anthropic เป็น WARROOM-CEO

งานดัดแปลงนี้เผยแพร่ภายใต้ **Apache License, Version 2.0** เช่นเดียวกัน ดูไฟล์ `LICENSE` สำหรับข้อความสัญญาอนุญาตฉบับเต็ม

### สรุปสิทธิ์ตาม Apache 2.0

| สิทธิ์ | รายละเอียด |
|--------|-----------|
| ✅ ใช้งานส่วนตัวและเชิงพาณิชย์ | ใช้ได้อย่างอิสระในทุกบริบท |
| ✅ ดัดแปลงและแจกจ่าย | สามารถแก้ไขและแชร์ต่อได้ |
| ✅ สร้างงานดัดแปลง | นำไปต่อยอดได้ภายใต้ license เดิมหรือที่เข้ากันได้ |

| เงื่อนไข | รายละเอียด |
|----------|-----------|
| 📋 ระบุการเปลี่ยนแปลง | ไฟล์ที่แก้ไขต้องมีหมายเหตุว่าถูกเปลี่ยนแปลง |
| 📋 คงไว้ซึ่งลิขสิทธิ์ต้นฉบับ | ต้องแนบประกาศลิขสิทธิ์ของ Anthropic ไว้ด้วย |
| 📋 แนบไฟล์ LICENSE | ต้องมีไฟล์ `LICENSE` ในทุกการแจกจ่าย |
| ❌ ห้ามใช้เครื่องหมายการค้า | ห้ามนำชื่อ Anthropic ไปใช้ทางการตลาดโดยไม่ได้รับอนุญาต |

---

*skill-creator Thai Edition — ดัดแปลงจาก Anthropic skill-creator โดย WARROOM-CEO*
