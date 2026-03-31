# Connectors (ตัวเชื่อมโยง)

## วิธีการอ้างอิง Tool

Plugin files ใช้ `~~category` เป็น placeholder สำหรับเครื่องมือที่ผู้ใช้เชื่อมต่อในหมวดหมู่นั้น ตัวอย่างเช่น `~~project tracker` อาจหมายถึง Linear, Asana, Jira หรือ tracker อื่นๆ ที่มี MCP server

ปลั๊กอินจะ **เป็น tool-agnostic** — อธิบายเวิร์กโฟลว์ในแง่ของหมวดหมู่ (project tracker, design, product analytics ฯลฯ) แทนที่จะเป็นผลิตภัณฑ์เฉพาะ `.mcp.json` มีการตั้งค่าเบื้องต้นของ MCP server เฉพาะ แต่ MCP server ใดๆ ในหมวดหมู่นั้นจะทำงานได้

## Connectors สำหรับปลั๊กอินนี้

| หมวดหมู่ | Placeholder | Included servers | ตัวเลือกอื่น |
|----------|-------------|-----------------|---------------|
| Calendar | `~~calendar` | Google Calendar | Microsoft 365 |
| Chat | `~~chat` | Slack | Microsoft Teams |
| Competitive intelligence | `~~competitive intelligence` | Similarweb | Crayon, Klue |
| Design | `~~design` | Figma | Sketch, Adobe XD |
| Email | `~~email` | Gmail | Microsoft 365 |
| Knowledge base | `~~knowledge base` | Notion | Confluence, Guru, Coda |
| Meeting transcription | `~~meeting transcription` | Fireflies | Gong, Dovetail, Otter.ai |
| Product analytics | `~~product analytics` | Amplitude, Pendo | Mixpanel, Heap, FullStory |
| Project tracker | `~~project tracker` | Linear, Asana, monday.com, ClickUp, Atlassian (Jira/Confluence) | Shortcut, Basecamp |
| User feedback | `~~user feedback` | Intercom | Productboard, Canny, UserVoice |
