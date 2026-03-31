# ตรวจสอบ Accessibility

**ประเภท**: User-invoked
**Trigger**: `/accessibility-review` + Figma URL, URL, หรือ description

## ภาพรวม

ตรวจสอบ design หรือหน้าเว็บสำหรับ WCAG 2.1 AA accessibility compliance นำเสนอการตรวจสอบครอบคลุม 4 หมวดหมู่:
- **Perceivable**: alt text, color contrast, semantic structure
- **Operable**: keyboard navigation, focus order, touch targets (≥44x44px)
- **Understandable**: error messages, labels, predictable behavior
- **Robust**: ARIA roles, name/role/value for all components

## Output

Audit report ที่มี:
- สรุปผล (จำนวนปัญหา, ระดับความรุนแรง)
- ตารางแยกตามหมวดหมู่ WCAG พร้อม severity badges
- ตารางการทดสอบ color contrast
- ลำดับ tab navigation
- Screen reader announcements
- ลำดับความสำคัญในการแก้ไข

## เชื่อมโยงกับ

- **design-critique**: ตรวจสอบ accessibility เป็นส่วนหนึ่งของ feedback
- **design-handoff**: รับรองการยืนยันความสอดคล้อง WCAG ก่อน dev handoff
- Figma MCP: ดึง color values, font sizes, touch targets จาก design
- Project tracker MCP: สร้างปัญหา accessibility สำหรับ implementation
