# Connectors (ภาษาไทย)

## วิธีที่ plugin อ้างอิงเครื่องมือ

ไฟล์ใน plugin ใช้ `~~category` เป็น placeholder สำหรับเครื่องมือที่ผู้ใช้เชื่อมต่อในหมวดนั้น ตัวอย่างเช่น `~~HRIS` อาจหมายถึง Workday, BambooHR หรือ HRIS อื่นที่มี MCP server

Plugin ออกแบบให้ **ไม่ผูกกับเครื่องมือเฉพาะ** — อธิบาย workflow ในรูปแบบหมวดหมู่ (HRIS, ATS, email ฯลฯ) แทนที่จะระบุผลิตภัณฑ์เจาะจง ไฟล์ `.mcp.json` กำหนด MCP server เริ่มต้นไว้ล่วงหน้า แต่ MCP server ใดก็ตามในหมวดนั้นสามารถใช้งานได้

## Connectors ของ Plugin นี้

| หมวดหมู่ | Placeholder | Server ที่รวมมา | ตัวเลือกอื่น |
|---------|-------------|----------------|-------------|
| ATS (ระบบสรรหาบุคลากร) | `~~ATS` | — | Greenhouse, Lever, Ashby, Workable |
| ปฏิทิน (Calendar) | `~~calendar` | Google Calendar | Microsoft 365 |
| แชท (Chat) | `~~chat` | Slack | Microsoft Teams |
| อีเมล (Email) | `~~email` | Gmail, Microsoft 365 | — |
| HRIS (ระบบข้อมูล HR) | `~~HRIS` | — | Workday, BambooHR, Rippling, Gusto |
| Knowledge Base | `~~knowledge base` | Notion, Atlassian (Confluence) | Guru, Coda |
| ข้อมูลค่าตอบแทน (Compensation data) | `~~compensation data` | — | Pave, Radford, Levels.fyi |
