# Connectors (คู่มือการเชื่อมต่อเครื่องมือ)

## MCP Server ในเครื่อง

Plugin นี้ใช้ **MCP server ในเครื่อง** แทนการเชื่อมต่อกับบริการภายนอก PDF server ทำงานบนเครื่องของคุณผ่าน `npx`

| หมวดหมู่ | Server | วิธีการทำงาน |
|---------|--------|-------------|
| PDF viewer & annotator | `@modelcontextprotocol/server-pdf` | Local stdio ผ่าน `npx` (ติดตั้งอัตโนมัติ) |

---

## ข้อกำหนด

- **Node.js เวอร์ชัน 18 ขึ้นไป**
- **การเชื่อมต่ออินเทอร์เน็ต** สำหรับ PDF ที่อยู่ online (arXiv, bioRxiv ฯลฯ)
- **ไม่ต้องใช้ API key หรือการยืนยันตัวตน** — server เริ่มต้นอัตโนมัติเมื่อโหลด plugin

---

*ดู CONNECTORS.md (ภาษาอังกฤษ) สำหรับข้อมูลทางเทคนิคที่ Claude ใช้ภายใน*
