# กลยุทธ์การค้นหา Knowledge MCP

รูปแบบการค้นหาสำหรับรวบรวมบริบทขององค์กรระหว่างการปรับแต่งปลั๊กอิน

## การค้นหาชื่อเครื่องมือ

**Source control (ระบบควบคุมเวอร์ชัน):**
- ค้นหา: "GitHub" OR "GitLab" OR "Bitbucket"
- ค้นหา: "pull request" OR "merge request"
- มองหา: ลิงก์ repository, การกล่าวถึง CI/CD

**Project management (การจัดการโปรเจกต์):**
- ค้นหา: "Asana" OR "Jira" OR "Linear" OR "Monday"
- ค้นหา: "sprint" AND "tickets"
- มองหา: ลิงก์งาน, การกล่าวถึง project board

**Chat (แชท):**
- ค้นหา: "Slack" OR "Teams" OR "Discord"
- มองหา: การกล่าวถึงช่อง, การอภิปรายเกี่ยวกับการเชื่อมต่อ

**Analytics (วิเคราะห์ข้อมูล):**
- ค้นหา: "Datadog" OR "Grafana" OR "Mixpanel"
- ค้นหา: "monitoring" OR "observability"
- มองหา: ลิงก์ dashboard, การกำหนดค่า alert

**Design (ออกแบบ):**
- ค้นหา: "Figma" OR "Sketch" OR "Adobe XD"
- มองหา: ลิงก์ไฟล์ออกแบบ, การอภิปราย handoff

**CRM (ระบบจัดการลูกค้า):**
- ค้นหา: "Salesforce" OR "HubSpot"
- มองหา: การกล่าวถึง deal, ลิงก์บันทึกลูกค้า

## การค้นหาค่าขององค์กร

**ID เวิร์กสเปซ/โปรเจกต์:**
- ค้นหาการเชื่อมต่อที่มีอยู่หรือลิงก์ที่บันทึกไว้
- มองหาเอกสารผู้ดูแล/การตั้งค่า

**แบบแผนของทีม:**
- ค้นหา: "story points" OR "estimation"
- ค้นหา: "workflow" OR "ticket status"
- มองหาเอกสารกระบวนการวิศวกรรม

**ชื่อช่อง/ทีม:**
- ค้นหา: "standup" OR "engineering" OR "releases"
- มองหารูปแบบการตั้งชื่อช่อง

## เมื่อไม่มี Knowledge MCP

หากไม่มี Knowledge MCP ที่กำหนดค่าไว้ ข้ามการค้นพบอัตโนมัติและใช้ AskUserQuestion สำหรับทุกหมวดหมู่โดยตรง หมายเหตุ: AskUserQuestion จะมีปุ่มข้ามและช่องข้อความอิสระเสมอ ดังนั้นไม่ต้องเพิ่มตัวเลือก "ไม่มี" หรือ "อื่นๆ"
