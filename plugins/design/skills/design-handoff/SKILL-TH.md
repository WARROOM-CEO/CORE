# Developer Handoff Specs

**ประเภท**: User-invoked
**Trigger**: `/design-handoff` + Figma URL หรือ design description

## ภาพรวม

สร้าง comprehensive developer handoff documentation จาก design พร้อมรายละเอียดการออกแบบทั้งหมด:
- **Visual Specs**: measurements, design tokens, responsive breakpoints
- **Interactions**: hover states, transitions, animations (duration, easing)
- **Content**: character limits, truncation, empty/loading/error states
- **Edge Cases**: content min/max, international text, slow connections
- **Accessibility**: focus order, ARIA labels, keyboard interactions

## Output

Handoff spec ที่มี:
- Overview (context ผู้ใช้)
- Layout grid/breakpoints
- Design tokens table (colors, spacing, typography)
- Components table (variants, props, special behavior)
- States and interactions table
- Responsive breakpoints table
- Edge cases checklist
- Animation/motion table
- Accessibility notes

## เชื่อมโยงกับ

- **design-critique**: ตรวจสอบก่อนที่จะสร้าง handoff
- **accessibility-review**: รวมค่าหมายเหตุ accessibility จาก audit
- Figma MCP: ดึง measurements, tokens, และ component specs แบบ exact
- Project tracker MCP: เชื่อมโยง handoff กับ implementation ticket
