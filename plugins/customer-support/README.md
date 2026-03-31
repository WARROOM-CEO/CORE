# Plugin Customer Support

ปลั๊กอิน customer support ออกแบบมาหลักสำหรับ [Cowork](https://claude.com/product/cowork) เพื่อช่วยทีม support ในการ triage tickets, ร่าง responses, escalate issues, ค้นคว้าข้อมูล customer context และสร้าง knowledge base articles — แปลงปัญหาที่แก้แล้วให้เป็น self-service content สำหรับ customers ที่เข้ามาในอนาคต

## การติดตั้ง

```
claude plugins add knowledge-work-plugins/customer-support
```

## ภาพรวมการทำงาน

Plugin นี้แปลง Claude ให้เป็น customer support co-pilot ด้วย 5 skills หลัก:

1. **Ticket Triage** — จัดหมวดหมู่ prioritize และส่งต่อ ticket ใหม่อย่างมีโครงสร้าง
2. **Customer Research** — ค้นคว้าข้อมูลจากหลายแหล่งพร้อม source attribution และ confidence scoring
3. **Draft Response** — ร่าง professional customer-facing responses ที่tailored ตามสถานการณ์
4. **Customer Escalation** — Package escalations สำหรับ engineering/product/leadership พร้อม reproduction steps
5. **KB Article** — ร่าง knowledge base articles จาก resolved issues เพื่อลด future ticket volume

## Skills ทั้งหมด

| Skill | ประเภท | Trigger | เชื่อมโยงกับ |
|-------|--------|---------|-----------|
| **ticket-triage** | User-invoked | `/ticket-triage <ticket or issue description>` | draft-response, customer-research, customer-escalation |
| **customer-research** | User-invoked | `/customer-research <question or topic>` | draft-response, ticket-triage, kb-article |
| **draft-response** | User-invoked | `/draft-response <situation description>` | ticket-triage, customer-research, customer-escalation, kb-article |
| **customer-escalation** | User-invoked | `/customer-escalation <issue summary> [customer name]` | ticket-triage, customer-research, draft-response, kb-article |
| **kb-article** | User-invoked | `/kb-article <resolved issue or ticket>` | ticket-triage, customer-research, draft-response |

### Ticket Triage — `/triage`

Triage และจัดลำดับความสำคัญ support ticket ใหม่ ผลลัพธ์คือ:
- Category (Bug, Feature Request, Billing, Account, How-to, Integration, Security, Data, Performance)
- Priority P1-P4 พร้อมเหตุผล
- Product area
- Routing recommendation (Tier 1, Tier 2, Engineering, Product, Security, Billing)
- Initial response draft
- Known issue status

**ใช้เมื่อ:** Ticket ใหม่เข้ามาต้องการ categorization หรือต้องการตรวจสอบ duplicate/known issue

### Customer Research — `/research`

ค้นคว้าข้อมูล multi-source (knowledge base, CRM, support history, chat, email, web) สำหรับคำถาม topic หรือ customer context ผลลัพธ์คือ:
- Direct answer (bottom-line-up-front)
- Confidence level (High/Medium/Low)
- Key findings from each source
- Source attribution ชัดเจน
- Context & nuance
- Gaps & unknowns
- Recommended next steps

**ใช้เมื่อ:** Customer ถามคำถามต้องค้นหา, สืบสวน bug ที่เคยรายงาน, หรือรวบรวม context ก่อนร่าง response

### Draft Response — `/draft-response`

ร่าง professional customer-facing response tailored ตามสถานการณ์ (product question, escalation, outage, bad news, billing, feature decline) ผลลัพธ์คือ:
- Draft response text
- Tone specification (Empathetic/Professional/Technical/Celebratory/Candid)
- Channel (Email/Ticket/Chat)
- Internal notes (rationale, things to verify, risk factors, follow-up needed)
- Quality checks (tone matches situation, no over-commitments, accurate references, clear next steps)

**ใช้เมื่อ:** ต้องร่าง response ต่อ customer หรือ escalation

### Customer Escalation — `/escalate`

Package escalation brief สำหรับ engineering/product/security/leadership พร้อม context ครบถ้วน, reproduction steps, business impact assessment ผลลัพธ์คือ:
- Severity (Critical/High/Medium)
- Target team
- Impact assessment (customers affected, workflow impact, revenue at risk, duration)
- Detailed issue description
- Reproduction steps (for bugs)
- Troubleshooting already tried
- Customer communication status
- What's needed (investigate, prioritize fix, make decision, approve exception)
- Supporting context

**ใช้เมื่อ:** Bug ต้องการ engineering attention, multiple customers report same issue, customer คุกคาม churn หรือ issue ค้างเกิน SLA

### KB Article — `/kb-article`

ร่าง knowledge base article จาก resolved issue, common question หรือ workaround ผลลัพธ์คือ:
- Article title (searchable)
- Article type (How-to/Troubleshooting/FAQ/Known Issue/Reference)
- Category & tags
- Audience
- Full article body (structured per type)
- Related articles
- Publishing notes

**ใช้เมื่อ:** Ticket resolution คุ้มค่าต่อการ document, คำถามเดิมปรากฏซ้ำ, workaround ต้อง publish หรือ known issue ต้อง communicate

## โครงสร้างไฟล์ — Bilingual Design Pattern

| ไฟล์ English | ไฟล์ Thai | วัตถุประสงค์ |
|-------------|----------|-----------|
| `.claude-plugin/plugin.json` | — | Plugin metadata (description ปรับปรุง) |
| `skills/*/SKILL.md` | `skills/*/SKILL-TH.md` | Skill definition (English) & Thai user-facing summary |
| `CONNECTORS.md` | `CONNECTORS-TH.md` | Tool reference guide (English) & Thai translation |
| `README.md` | README.md (rewritten) | Plugin documentation in Thai |

### SKILL.md Files
- **English original:** Contains full workflow documentation, best practices, templates
- **Language directive:** Brief statement that all user-facing output must be in Thai
- **SKILL-TH.md companion:** Thai-language summary of skill, key features, output format, connector hints

### CONNECTORS Files
- **CONNECTORS.md:** English explanation of how tool references work, connector categories
- **CONNECTORS-TH.md:** Thai translation of same content with full table and details

## สัญญาอนุญาต

Plugin นี้ใช้ Apache License 2.0

| สิทธิ | ✅/❌ |
|------|------|
| **ใช้งานเชิงพาณิชย์** | ✅ ได้ |
| **ปรับแต่ง/Modify** | ✅ ได้ |
| **배포 (Distribute)** | ✅ ได้ |
| **ใช้เอกชน (Private use)** | ✅ ได้ |
| **Sublicense** | ✅ ได้ |
| **รับประกัน (Warranty)** | ❌ ไม่มี |
| **Liability** | ❌ ไม่มี |
| **แจ้งเปลี่ยนแปลง** | ⚠️ จำเป็น — ต้องแจ้ง Apache 2.0 สัญญาอนุญาต |
| **ระบุผู้ได้รับอนุญาต** | ⚠️ จำเป็น — ต้องระบุผู้ที่มีลิขสิทธิ์ |

## การกำหนดค่า

Plugin ทำงานจากกล่องด้วย included MCP connections ได้เลย สำหรับประสบการณ์ที่ดีที่สุด ให้เชื่อมต่อเครื่องมือเพิ่มเติมผ่าน Claude settings:

1. **Support platform**: เพิ่มระบบ ticketing เพื่อ ticket history และ customer context
2. **Knowledge base**: เพิ่ม wiki เพื่อเอกสารภายในและ KB articles ที่มีอยู่
3. **Project tracker**: เพิ่ม issue tracker เพื่อ bug reports และ feature requests
4. **CRM**: เพิ่ม CRM เพื่อรายละเอียดบัญชีและข้อมูล contact

หากไม่มี connectors เหล่านี้ plugin จะขอ context ด้วยตนเอง และให้กรอบการทำงานและเทมเพลตที่สามารถกรอก context ด้วยตัวเอง
