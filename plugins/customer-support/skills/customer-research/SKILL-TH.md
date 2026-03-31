# /customer-research

ทักษะค้นคว้าข้อมูล multi-source สำหรับคำถามหรือหัวข้อของ customer

**ประเภท:** User-invoked
**Trigger:** `/customer-research <question or topic>`

## ภาพรวม

ใช้ skill นี้เพื่อค้นคว้าข้อมูลจากหลายแหล่งเกี่ยวกับคำถาม topic หรือบริบทของ customer ผลลัพธ์คือ structured research brief พร้อม source attribution, confidence scoring, key findings, และคำแนะนำ next steps

## ใช้เมื่อ

- Customer ถามคำถามที่ต้องค้นหาคำตอบ
- สืบสวน bug ที่อาจมีรายงานก่อนหน้า
- ตรวจสอบว่า customer ได้รับการบอกอะไรไปก่อนหน้า
- รวบรวม background context ก่อนร่าง response

## ผลลัพธ์หลัก

**Structured Research Brief** ประกอบด้วย:
- Direct answer to the question (คำตอบแบบ bottom-line-up-front)
- Confidence level (High/Medium/Low)
- Key findings from each source
- Context & nuance (ข้อควรระวัง, edge cases)
- Source attribution ที่ชัดเจน
- Gaps & unknowns (ไม่มีข้อมูลอะไร)
- Recommended next steps

## Research Sources (ลำดับความสำคัญ)

**Tier 1 — Official Internal Sources:**
- Knowledge base (product docs, runbooks, FAQs)
- Cloud storage (internal documents, specs, guides)
- Product roadmap

**Tier 2 — Organizational Context:**
- CRM notes (account notes, activity history)
- Support platform (previous resolutions, known issues)
- Meeting notes

**Tier 3 — Team Communications:**
- Chat channels (relevant discussions)
- Email archives
- Calendar notes

**Tier 4 — External Sources:**
- Web search (official docs, blog posts)
- Public knowledge bases, help centers
- Third-party documentation

**Tier 5 — Inference:**
- Similar situations, analogous customers
- General best practices, industry standards

## Confidence Levels

| Level | ความหมาย | ตัวอย่าง |
|-------|---------|---------|
| **High** | Confirmed by official docs or multiple sources | "ผลลัพธ์มาจากเอกสารอย่างเป็นทางการ" |
| **Medium** | Found in informal sources, single source | "ข้อมูลมาจาก CRM แต่ไม่ได้ยืนยันจากเอกสาร" |
| **Low** | Inferred from related info, outdated sources | "ฉันไม่พบคำตอบชัดเจน อาจต้องตรวจสอบกับ SME" |

## เชื่อมโยงกับ

- `/draft-response` — เมื่อต้อง draft response ถึง customer โดยใช้ research findings
- `/ticket-triage` — เมื่อต้องการ context เพิ่มเติมสำหรับ triage ticket
- `/kb-article` — เมื่อ research findings ควร document เป็น KB article
