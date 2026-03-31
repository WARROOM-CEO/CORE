# ปลั๊กอิน Product Management

ปลั๊กอิน product management ที่ออกแบบสำหรับ [Cowork](https://claude.com/product/cowork) ซึ่งเป็นแอปพลิเคชั่นเดสก์ท็อป agentic ของ Anthropic — แม้ว่าจะทำงานใน Claude Code ได้เช่นกัน ครอบคลุมเวิร์กโฟลว์ PM เต็มตัว: เขียน feature specs, บริหาร roadmaps, สื่อสารกับ stakeholders, synthesize user research, วิเคราะห์คู่แข่ง และ track product metrics

ปลั๊กอินนี้เขียน feature specs, วางแผน roadmap และสังเคราะห์ user research ได้เร็วขึ้น อัปเดตผู้มีส่วนได้ส่วนเสียและติดตาม competitive landscape อย่างมีประสิทธิภาพ

## ภาพรวมการทำงาน

### สำหรับ Product Manager
PM ใช้ skill นี้เพื่อ:
- เขียน PRDs ที่มีโครงสร้าง จาก problem statement หรือ feature idea
- สร้าง roadmaps, update priorities, map dependencies
- Generate stakeholder updates ที่เหมาะกับ audience
- Synthesize user research เป็น actionable insights
- Analyze competitors และสร้าง battle cards
- Track product metrics, identify trends, recommend actions
- Brainstorm ideas, test assumptions, explore strategies

### สำหรับ Engineering Leader
- Pull roadmap status, identify blockers, plan sprints
- Review metrics, track progress against OKRs
- Create sprint plans with clear scope and capacity
- Communicate risks up to leadership

### สำหรับ Design
- Pull feature specs เมื่อ writing design briefs
- Review roadmap timelines, plan design work
- Reference competitive analysis when evaluating positioning

### สำหรับ Customer Success / Support
- Monitor stakeholder updates และ launch announcements
- Understand roadmap priorities เพื่ออธิบายให้ customers
- Synthesize support tickets เป็น product insights

## Skills ทั้งหมด

| Skill | ประเภท | Trigger | เชื่อมโยงกับ |
|-------|-------|---------|----------|
| Competitive Brief | User-invoked | `/competitive-brief <competitor or feature area>` | Competitive intelligence, Knowledge base, Chat |
| Metrics Review | User-invoked | `/metrics-review <time period or metric focus>` | Product analytics, Project tracker, Knowledge base |
| Product Brainstorming | Model-invoked | `/brainstorm` (or auto-triggered) | Knowledge base, Product analytics, Project tracker, Chat |
| Roadmap Update | User-invoked | `/roadmap-update <update description>` | Project tracker, Chat, Calendar |
| Sprint Planning | User-invoked | `/sprint-planning [sprint name or date range]` | Project tracker, Calendar, Chat |
| Stakeholder Update | User-invoked | `/stakeholder-update <update type and audience>` | Project tracker, Chat, Meeting transcription, Knowledge base |
| Synthesize Research | User-invoked | `/synthesize-research <research topic or question>` | Knowledge base, User feedback, Product analytics, Meeting transcription |
| Write Spec | User-invoked | `/write-spec <feature or problem statement>` | Project tracker, Knowledge base, Design |
| Brainstorm (Command) | User-invoked | `/brainstorm <topic, problem, or idea>` | Knowledge base, Product analytics, Project tracker, Chat |

### Skill Descriptions

**Competitive Brief** — สร้าง competitive analysis brief สำหรับคู่แข่งหรือ feature area ใช้เมื่อต้องการข้อมูลสำหรับ product strategy, sales battle cards, board materials หรือตัดสินใจว่าจะ differentiate หรือ achieve parity

**Metrics Review** — วิเคราะห์ product metrics พร้อม trend analysis และ actionable insights ใช้เมื่อ review metrics รายสัปดาห์/เดือน/ไตรมาส สืบสวน spike หรือ drop หรือสร้าง scorecard พร้อม recommended actions

**Roadmap Update** — อัปเดต สร้าง หรือปรับลำดับความสำคัญ product roadmap ใช้เมื่อเพิ่ม initiative ใหม่ เปลี่ยน priority หลังได้ข้อมูลใหม่ หรือสร้าง Now/Next/Later view ตั้งแต่ต้น

**Sprint Planning** — วางแผน sprint — กำหนด scope, ประเมิน capacity, ตั้งเป้าหมาย และร่าง sprint plan ใช้เมื่อเริ่ม sprint ใหม่ ตัดสินใจว่างานไหน P0 vs. stretch หรือจัดการ carryover

**Stakeholder Update** — สร้าง stakeholder update ที่เหมาะกับผู้รับและความถี่ ใช้เมื่อเขียน status รายสัปดาห์/เดือนให้ leadership ประกาศ launch escalate risk หรือแปลง progress เป็นเวอร์ชัน exec-brief, engineering-detail หรือ customer-facing

**Synthesize Research** — สังเคราะห์ user research จาก interviews, surveys และ feedback เป็น insights ที่มีโครงสร้าง ใช้เมื่อมี interview notes, survey responses หรือ support tickets ที่ต้องทำความเข้าใจ หรือแปลง feedback เป็น roadmap recommendations

**Write Spec** — เขียน feature spec หรือ PRD จาก problem statement หรือ feature idea ใช้เมื่อต้องการเปลี่ยน idea คลุมเครือให้เป็นเอกสาร structured กำหนด goals/non-goals, success metrics และ acceptance criteria

**Product Brainstorming** — คู่คิด PM ที่ challenge assumptions, ถามคำถามยากๆ และผลักดัน ideas ให้ไปไกลขึ้น ช่วย explore problem spaces, generate ideas และ stress-test thinking ก่อนเขียน spec

**Brainstorm (Command)** — brainstorm ใน product topic กับ thinking partner ที่ opinionated ใช้เมื่อ explore opportunity areas, ทดสอบ assumptions, apply PM frameworks (HMW, JTBD, First Principles) หรือต้องการ sparring partner ก่อนมุ่งไปทิศทางใด

## โครงสร้างไฟล์

| English File | Thai File | วัตถุประสงค์ |
|--------------|-----------|-----------|
| `skills/competitive-brief/SKILL.md` | `skills/competitive-brief/SKILL-TH.md` | Competitive analysis workflow + Thai summary |
| `skills/metrics-review/SKILL.md` | `skills/metrics-review/SKILL-TH.md` | Metrics analysis workflow + Thai summary |
| `skills/product-brainstorming/SKILL.md` | `skills/product-brainstorming/SKILL-TH.md` | Brainstorming partner guidance + Thai summary |
| `skills/roadmap-update/SKILL.md` | `skills/roadmap-update/SKILL-TH.md` | Roadmap management + Thai summary |
| `skills/sprint-planning/SKILL.md` | `skills/sprint-planning/SKILL-TH.md` | Sprint planning process + Thai summary |
| `skills/stakeholder-update/SKILL.md` | `skills/stakeholder-update/SKILL-TH.md` | Status update templates + Thai summary |
| `skills/synthesize-research/SKILL.md` | `skills/synthesize-research/SKILL-TH.md` | Research synthesis methods + Thai summary |
| `skills/write-spec/SKILL.md` | `skills/write-spec/SKILL-TH.md` | PRD writing guide + Thai summary |
| `commands/brainstorm.md` | `commands/brainstorm-TH.md` | Brainstorm command workflow + Thai summary |
| `CONNECTORS.md` | `CONNECTORS-TH.md` | Tool integration guide + Thai translation |
| `.claude-plugin/plugin.json` | — | Plugin metadata (Thai description) |
| `README.md` (English version) | `README.md` (Thai version) | Plugin overview (this file) |

## สัญญาอนุญาต

ปลั๊กอินนี้ได้รับอนุญาตภายใต้ [Apache License 2.0](LICENSE)

| สิทธิ | ✅ อนุญาต | ❌ ห้าม |
|------|---------|--------|
| ใช้ในเชิงพาณิชย์ | ✅ | — |
| ปรับแต่ง / ขยายตัว | ✅ | — |
| จัดจำหน่าย | ✅ | — |
| ใช้เป็นส่วนประกอบของสินค้า | ✅ | — |
| ปรับปรุงอัปเดต | — | ❌ (ต้องระบุการเปลี่ยนแปลง) |
| ลบประกาศลิขสิทธิ์ | — | ❌ |
| ให้ความรับประกัน | — | ❌ (ให้เป็น "as-is") |
