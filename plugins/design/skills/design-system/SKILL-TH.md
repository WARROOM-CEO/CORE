# Design System Management

**ประเภท**: User-invoked
**Trigger**: `/design-system [audit | document | extend] <component or system>`

## ภาพรวม

จัดการระบบ design — audit ความสอดคล้องกัน document components หรือออกแบบ patterns ใหม่

### Audit Mode
ตรวจตามระบบเต็ม:
- Naming consistency (คำนำหน้า, suffix, naming conventions)
- Token coverage (ค่า hardcoded ที่พบ)
- Component completeness (states, variants, documentation)
- Score/rating overall

### Document Mode
เขียน documentation สำหรับ component:
- Description & use cases
- Variants table
- Props/Properties table
- States (default, hover, active, disabled, loading)
- Accessibility (role, keyboard, screen reader)
- Do's and Don'ts
- Code examples

### Extend Mode
ออกแบบ component/pattern ใหม่:
- Problem it solves
- Existing patterns comparison
- Proposed API & props
- Variants & states
- Tokens used
- Accessibility requirements
- Open questions

## Output

Audit: summary report พร้อม score, inconsistencies, token usage, priority actions
Document: component spec พร้อม variants, props, states, accessibility
Extend: design proposal พร้อม API, variants, states, accessibility

## เชื่อมโยงกับ

- **design-critique**: ตรวจสอบความสอดคล้องกับระบบ
- Figma MCP: audit components โดยตรง, inspect naming/variants/tokens
- Knowledge base MCP: ค้นหา documentation และ usage guidelines
