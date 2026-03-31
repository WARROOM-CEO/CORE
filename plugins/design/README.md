# ปลั๊กอิน Design

ปลั๊กอิน design productivity ที่ออกแบบสำหรับ [Cowork](https://claude.com/product/cowork) ของ Anthropic แอปพลิเคชน desktop agentic — แม้ว่าจะใช้ได้กับ Claude Code ด้วย ช่วยด้านการวิจารณ์ design, การจัดการระบบ design, การเขียน UX copy, accessibility, research synthesis และ developer handoff ทำงานกับทีม design ใด ๆ — standalone ด้วยอินพุตของคุณ, supercharged เมื่อคุณเชื่อมต่อ Figma และเครื่องมืออื่น ๆ

## ภาพรวมการทำงาน

ปลั๊กอิน design ช่วยให้ทีม design สามารถ:
- **ประเมินผล designs** ตามหลายมิติ (usability, hierarchy, consistency, accessibility)
- **จัดการระบบ design** — audit ความสอดคล้องกัน document components, extend patterns
- **เขียน UX copy** — CTAs, error messages, empty states, onboarding
- **ตรวจสอบ accessibility** — WCAG 2.1 AA compliance audits
- **สังเคราะห์ research** — convert transcripts/surveys into actionable insights
- **สร้าง developer specs** — comprehensive handoff documentation

ทุก skill ทำงาน **standalone** (อธิบายหรือ paste screenshots) และได้รับการเพิ่มประสิทธิภาพเมื่อคุณเชื่อมต่อ MCP connectors

## Skills ทั้งหมด

| Skill | ประเภท | Trigger | เชื่อมโยงกับ |
|-------|--------|---------|-----------|
| `accessibility-review` | User-invoked | `/accessibility-review <Figma URL, URL, or description>` | design-critique, design-handoff, Figma, Project tracker |
| `design-critique` | User-invoked | `/design-critique <Figma URL, screenshot, or description>` | accessibility-review, design-handoff, Figma, User feedback |
| `design-handoff` | User-invoked | `/design-handoff <Figma URL or design description>` | design-critique, accessibility-review, Figma, Project tracker |
| `design-system` | User-invoked | `/design-system [audit \| document \| extend] <component or system>` | design-critique, Figma, Knowledge base |
| `research-synthesis` | User-invoked | `/research-synthesis <research data, transcripts, or survey results>` | user-research, User feedback, Product analytics, Knowledge base |
| `user-research` | Model-invoked | Auto-triggered when planning/conducting research | research-synthesis |
| `ux-copy` | User-invoked | `/ux-copy <context or copy to review>` | design-critique, design-handoff, Knowledge base, Design tool |

### คำอธิบาย Skills

**accessibility-review**: ตรวจสอบ WCAG 2.1 AA accessibility ของ design หรือหน้าเว็บ เรียกใช้เมื่อต้องการ audit color contrast, keyboard navigation, touch target size หรือ screen reader behavior ก่อน handoff สร้าง audit report ที่ครอบคลุม 4 หมวดหมู่ (Perceivable, Operable, Understandable, Robust) พร้อม severity levels, color contrast tables, keyboard navigation tests และ screen reader checks

**design-critique**: รับ structured feedback ด้านการออกแบบในแง่ usability, hierarchy และ consistency เรียกใช้เมื่อ share Figma link หรือ screenshot เพื่อรับ feedback ในทุก stage ตั้งแต่ exploration ถึง final polish ติดตามกรอบการประเมิน 5 มิติ: first impression, usability, visual hierarchy, consistency, accessibility

**design-handoff**: สร้าง developer handoff specs จาก design เมื่อพร้อมส่งต่อ engineering ครอบคลุม layout, design tokens, component props, interaction states, responsive breakpoints, edge cases และ animations สร้าง comprehensive spec sheet พร้อม measurements, states/interactions, responsive behavior, edge cases และ accessibility notes

**design-system**: Audit, document หรือ extend design system ใช้เมื่อตรวจหา naming inconsistencies, เขียน documentation สำหรับ component variants/states/accessibility หรือออกแบบ pattern ใหม่ที่เข้ากับ system ให้ audit score, document component specs พร้อม variants/props/states/accessibility, หรือ design new component proposals

**research-synthesis**: สังเคราะห์ user research เป็น themes, insights และ recommendations ใช้เมื่อมี interview transcripts, survey results, usability test notes, support tickets หรือ NPS responses ที่ต้องการ distill เป็น patterns และ next steps สร้าง synthesis report พร้อม key themes, user segments, insights→opportunities matrix และ priority recommendations

**user-research**: วางแผน ดำเนินการ และสังเคราะห์ user research studies เรียกใช้เมื่อต้องการ research plan, interview guide, usability test, survey design หรือ research questions ระบบอัตโนมัติเมื่อทีมต้องการความช่วยเหลือในการวิจัย ให้ research methods, interview guide structure, analysis frameworks และ deliverables checklist

**ux-copy**: เขียนหรือ review UX copy — microcopy, error messages, empty states, CTAs เรียกใช้เมื่อต้องการ name CTA, ร่าง confirmation dialog, เติม empty state หรือเขียน onboarding text สร้าง copy recommendations พร้อม alternatives, rationale และ localization notes

## โครงสร้างไฟล์

| English File | Thai File | วัตถุประสงค์ |
|--------------|-----------|-----------|
| `plugin.json` | — | Plugin metadata, version, Thai description |
| `README.md` | — | This file (entire plugin guide in Thai) |
| `CONNECTORS.md` | `CONNECTORS-TH.md` | Tool categories and MCP integrations |
| `skills/accessibility-review/SKILL.md` | `skills/accessibility-review/SKILL-TH.md` | WCAG audit skill + Thai summary |
| `skills/design-critique/SKILL.md` | `skills/design-critique/SKILL-TH.md` | Design feedback skill + Thai summary |
| `skills/design-handoff/SKILL.md` | `skills/design-handoff/SKILL-TH.md` | Developer handoff skill + Thai summary |
| `skills/design-system/SKILL.md` | `skills/design-system/SKILL-TH.md` | Design system management skill + Thai summary |
| `skills/research-synthesis/SKILL.md` | `skills/research-synthesis/SKILL-TH.md` | Research synthesis skill + Thai summary |
| `skills/user-research/SKILL.md` | `skills/user-research/SKILL-TH.md` | Research planning skill + Thai summary |
| `skills/ux-copy/SKILL.md` | `skills/ux-copy/SKILL-TH.md` | UX writing skill + Thai summary |

### Bilingual Design Pattern

- **SKILL.md files**: Thai `description:` frontmatter + language directive block
- **SKILL-TH.md files**: Thai user-facing summaries (ประเภท, Trigger, ภาพรวม, Output, เชื่อมโยงกับ)
- **CONNECTORS-TH.md**: Thai translation of CONNECTORS.md
- **README.md**: Entire guide rewritten in Thai

## สัญญาอนุญาต

Apache 2.0 License

| สิทธิ | ✅/❌ | หมายเหตุ |
|------|-------|--------|
| ใช้เชิงพาณิชย์ | ✅ | ใช้ได้ |
| ปรับเปลี่ยน | ✅ | ช่วยเหลือและแจกจ่ายได้ |
| จำหน่าย | ✅ | ภายใต้เงื่อนไข Apache 2.0 |
| ใช้เป็นส่วนตัว | ✅ | ปลอดภัยสำหรับใช้ส่วนตัว |
| Liability | ❌ | ไม่มีการรับประกัน |
| สิทธิบัตร | ✅ | ได้รับอนุญาต grant of patent rights |

ดูรายละเอียดเพิ่มเติมได้ใน [Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0)
