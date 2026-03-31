# Connectors (ตัวเชื่อมต่อ)

## วิธีการอ้างอิงเครื่องมือ

ไฟล์ปลั๊กอินใช้ `~~category` เป็น placeholder สำหรับเครื่องมือที่ผู้ใช้เชื่อมต่อในหมวดหมู่นั้น ตัวอย่างเช่น `~~design tool` อาจหมายถึง Figma, Sketch, หรือเครื่องมือออกแบบอื่น ๆ ที่มี MCP server

ปลั๊กอินเป็น **tool-agnostic** — อธิบายเวิร์กโฟลว์ในแง่ของหมวดหมู่ (design tool, project tracker, user feedback ฯลฯ) แทนที่จะเป็นผลิตภัณฑ์เฉพาะ `.mcp.json` ตั้งค่า MCP servers เบื้องต้น แต่ MCP server ใด ๆ ในหมวดหมู่นั้นจะใช้ได้

## ตัวเชื่อมต่อสำหรับปลั๊กอินนี้

| หมวดหมู่ | Placeholder | Included Servers | ตัวเลือกอื่น ๆ |
|----------|-------------|-----------------|---------------|
| Chat | `~~chat` | Slack | Microsoft Teams |
| Design tool | `~~design tool` | Figma | Sketch, Adobe XD, Framer |
| Knowledge base | `~~knowledge base` | Notion | Confluence, Guru, Coda |
| Project tracker | `~~project tracker` | Linear, Asana, Atlassian (Jira/Confluence) | Shortcut, ClickUp |
| User feedback | `~~user feedback` | Intercom | Productboard, Canny, UserVoice, Dovetail |
| Product analytics | `~~product analytics` | — | Amplitude, Mixpanel, Heap, FullStory |
