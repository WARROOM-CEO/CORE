# Connectors (ภาษาไทย)

## วิธีที่ plugin อ้างอิงเครื่องมือ

ไฟล์ใน plugin ใช้ `~~category` เป็น placeholder สำหรับเครื่องมือที่ผู้ใช้เชื่อมต่อในหมวดนั้น ตัวอย่างเช่น `~~data warehouse` อาจหมายถึง Snowflake, BigQuery หรือ data warehouse อื่นที่มี MCP server

Plugin ออกแบบให้ **ไม่ผูกกับเครื่องมือเฉพาะ** — อธิบาย workflow ในรูปแบบหมวดหมู่ (data warehouse, chat, ERP ฯลฯ) แทนที่จะระบุผลิตภัณฑ์เจาะจง ไฟล์ `.mcp.json` กำหนด MCP server เริ่มต้นไว้ล่วงหน้า แต่ MCP server ใดก็ตามในหมวดนั้นสามารถใช้งานได้

## Connectors ของ Plugin นี้

| หมวดหมู่ | Placeholder | Server ที่รวมมา | ตัวเลือกอื่น |
|---------|-------------|----------------|-------------|
| Data Warehouse | `~~data warehouse` | Snowflake\*, Databricks\*, BigQuery | Redshift, PostgreSQL |
| อีเมล (Email) | `~~email` | Microsoft 365 | — |
| Office Suite | `~~office suite` | Microsoft 365 | — |
| แชท (Chat) | `~~chat` | Slack | Microsoft Teams |
| ERP / Accounting | `~~erp` | — (ยังไม่มี MCP server ที่รองรับ) | NetSuite, SAP, QuickBooks, Xero |
| Analytics / BI | `~~analytics` | — (ยังไม่มี MCP server ที่รองรับ) | Tableau, Looker, Power BI |

\* Placeholder — MCP URL ยังไม่ได้กำหนดค่า
