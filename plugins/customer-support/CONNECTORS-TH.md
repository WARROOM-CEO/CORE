# Connectors - ตัวเชื่อมต่อเครื่องมือ

## วิธีการอ้างอิงเครื่องมือ

ไฟล์ plugin ใช้ `~~category` เป็น placeholder สำหรับเครื่องมือที่ user เชื่อมต่อในแต่ละหมวดหมู่ ตัวอย่างเช่น `~~support platform` อาจหมายถึง Intercom, Zendesk, หรือเครื่องมือ support อื่น ๆ ที่มี MCP server

Plugins เป็น **tool-agnostic** — อธิบายเวิร์กโฟลว์ในแง่ของหมวดหมู่ (support platform, CRM, chat ฯลฯ) แทนที่จะเป็นผลิตภัณฑ์เฉพาะ `.mcp.json` ก่อนกำหนดค่า MCP servers เฉพาะ แต่ MCP server ใด ๆ ในแต่ละหมวดหมู่ก็ใช้ได้

## Connectors สำหรับ Plugin นี้

| หมวดหมู่ | Placeholder | Servers ที่รวมมา | ตัวเลือกอื่น ๆ |
|--------|-------------|------------|------------|
| **Chat** | `~~chat` | Slack | Microsoft Teams |
| **Email** | `~~email` | Microsoft 365 | — |
| **Cloud storage** | `~~cloud storage` | Microsoft 365 | — |
| **Support platform** | `~~support platform` | Intercom | Zendesk, Freshdesk, HubSpot Service Hub |
| **CRM** | `~~CRM` | HubSpot | Salesforce, Pipedrive |
| **Knowledge base** | `~~knowledge base` | Guru, Notion | Confluence, Help Scout |
| **Project tracker** | `~~project tracker` | Atlassian (Jira/Confluence) | Linear, Asana |

## รายละเอียดของเครื่องมือแต่ละหมวดหมู่

### Chat — `~~chat`
**สำหรับ:** การสนทนาภายในและ context จากช่อง customer
**รวมมา:** Slack
**ตัวเลือกอื่น ๆ:** Microsoft Teams

ใช้เพื่อ:
- ค้นหาการอภิปรายเกี่ยวกับ customer หรือปัญหา
- ดูว่า teammates เคยตอบคำถามนี้ก่อนหน้า
- รวบรวม context จากการอภิปรายทีม
- ตรวจสอบการแนะนำจาก product/engineering/leadership

### Email — `~~email`
**สำหรับ:** การติดต่อกับ customer และการขึ้นต่อกัน
**รวมมา:** Microsoft 365
**ตัวเลือกอื่น ๆ:** —

ใช้เพื่อ:
- ดูการติดต่อก่อนหน้า customer
- ตรวจสอบสิ่งที่สัญญาไว้ก่อนหน้า
- ศึกษาสไตล์การสื่อสารของ customer
- ค้นหา context จากเธรดอีเมล

### Cloud Storage — `~~cloud storage`
**สำหรับ:** เอกสารภายในและวิธีปฏิบัติ
**รวมมา:** Microsoft 365
**ตัวเลือกอื่น ๆ:** —

ใช้เพื่อ:
- ค้นหาเอกสารข้อมูลจำเพาะ
- ดูเอกสารขั้นตอน (runbooks) ภายใน
- รวบรวมเนื้อหาวิธีปฏิบัติ
- ศึกษาแนวทางนโยบาย

### Support Platform — `~~support platform`
**สำหรับ:** ประวัติ ticket และบริบท customer
**รวมมา:** Intercom
**ตัวเลือก :** Zendesk, Freshdesk, HubSpot Service Hub

ใช้เพื่อ:
- ค้นหา ticket ที่คล้ายกันหรือ duplicate
- ดูประวัติการแก้ไขปัญหาของ customer
- ตรวจสอบ known issues และ workarounds
- ดึง conversation history ของ customer

### CRM — `~~CRM`
**สำหรับ:** รายละเอียดบัญชีและ context contact
**รวมมา:** HubSpot
**ตัวเลือกอื่น ๆ:** Salesforce, Pipedrive

ใช้เพื่อ:
- ดูรายละเอียดบัญชี (plan level, ARR)
- ตรวจสอบประวัติกิจกรรม customer
- ดูว่า customer ถามอะไรไปก่อนหน้า
- เข้าใจโอกาส opportunity และบริบทธุรกิจ

### Knowledge Base — `~~knowledge base`
**สำหรับ:** เอกสาร internal KB และบทความ
**รวมมา:** Guru, Notion
**ตัวเลือกอื่น ๆ:** Confluence, Help Scout

ใช้เพื่อ:
- ค้นหาเอกสาร KB ที่มีอยู่
- ตรวจสอบ how-to guides และ troubleshooting articles
- ดูข้อมูลรูปแบบทั่วไป (FAQs)
- ค้นหา known issues ที่ published

### Project Tracker — `~~project tracker`
**สำหรับ:** bug reports และ feature requests
**รวมมา:** Atlassian (Jira/Confluence)
**ตัวเลือกอื่น ๆ:** Linear, Asana

ใช้เพื่อ:
- ค้นหา bug reports ที่เกี่ยวข้อง
- ตรวจสอบ feature request และความถี่
- ดูสถานะ engineering ปัจจุบัน
- ติดตามการแก้ไขที่อยู่ระหว่างการดำเนินการ

## เคล็ดลับการตั้งค่า

- เชื่อมต่อเครื่องมือให้มากที่สุด เพื่อให้ plugin มีข้อมูล context ครบถ้วน
- หากเครื่องมือสำคัญไม่เชื่อมต่อ ให้ขอให้ user ระบุ context ด้วยตนเอง
- ใช้ placeholders `~~category` ใน SKILL.md — ค่าจริงมาจากการตั้งค่า user
- หากไม่มี connector ใดเชื่อมต่อ plugin ก็ยังทำงานได้ แต่อาจต้องให้ customer context ด้วยตนเอง
