# การค้นพบและเชื่อมต่อ MCP

วิธีค้นหาและเชื่อมต่อ MCP ระหว่างการปรับแต่งปลั๊กอิน

## เครื่องมือที่ใช้ได้

### `search_mcp_registry`
ค้นหาไดเรกทอรี MCP สำหรับ connector ที่มีอยู่

**Input:** `{ "keywords": ["array", "of", "search", "terms"] }`

**Output:** ผลลัพธ์สูงสุด 10 รายการ แต่ละรายการมี:
- `name`: ชื่อแสดงผลของ MCP
- `description`: คำอธิบายสั้นหนึ่งบรรทัด
- `tools`: รายชื่อเครื่องมือที่ MCP ให้บริการ
- `url`: URL endpoint ของ MCP (ใช้ใน `.mcp.json`)
- `directoryUuid`: UUID สำหรับใช้กับ suggest_connectors
- `connected`: Boolean - ผู้ใช้เชื่อมต่อ MCP นี้แล้วหรือยัง

### `suggest_connectors`
แสดงปุ่มเชื่อมต่อเพื่อให้ผู้ใช้ติดตั้ง/เชื่อมต่อ MCP

**Input:** `{ "directoryUuids": ["uuid1", "uuid2"] }`

**Output:** แสดง UI พร้อมปุ่มเชื่อมต่อสำหรับแต่ละ MCP

## การแมปหมวดหมู่-คีย์เวิร์ด

| หมวดหมู่ | คีย์เวิร์ดค้นหา |
|----------|-----------------|
| `project-management` (การจัดการโปรเจกต์) | `["asana", "jira", "linear", "monday", "tasks"]` |
| `software-coding` (การเขียนโค้ด) | `["github", "gitlab", "bitbucket", "code"]` |
| `chat` (แชท) | `["slack", "teams", "discord"]` |
| `documents` (เอกสาร) | `["google docs", "notion", "confluence"]` |
| `calendar` (ปฏิทิน) | `["google calendar", "calendar"]` |
| `email` (อีเมล) | `["gmail", "outlook", "email"]` |
| `design-graphics` (ออกแบบกราฟิก) | `["figma", "sketch", "design"]` |
| `analytics-bi` (วิเคราะห์ข้อมูล) | `["datadog", "grafana", "analytics"]` |
| `crm` (ระบบจัดการลูกค้า) | `["salesforce", "hubspot", "crm"]` |
| `wiki-knowledge-base` (วิกิ/ฐานความรู้) | `["notion", "confluence", "outline", "wiki"]` |
| `data-warehouse` (คลังข้อมูล) | `["bigquery", "snowflake", "redshift"]` |
| `conversation-intelligence` (ระบบวิเคราะห์การสนทนา) | `["gong", "chorus", "call recording"]` |

## ขั้นตอนการทำงาน

1. **ค้นหาจุดปรับแต่ง**: มองหาค่าที่ขึ้นต้นด้วย `~~` (เช่น `~~Jira`)
2. **ตรวจสอบผลการค้นพบจากขั้นตอนก่อนหน้า**: ทราบแล้วหรือยังว่าใช้เครื่องมืออะไร?
   - **ใช่**: ค้นหาเครื่องมือเฉพาะนั้นเพื่อรับ `url` ข้ามไปขั้นตอน 5
   - **ไม่**: ดำเนินการต่อขั้นตอน 3
3. **ค้นหา**: เรียก `search_mcp_registry` ด้วยคีย์เวิร์ดที่แมปไว้
4. **นำเสนอตัวเลือกและถามผู้ใช้**: แสดงผลลัพธ์ทั้งหมด ถามว่าใช้ตัวไหน
5. **เชื่อมต่อหากจำเป็น**: ถ้ายังไม่ได้เชื่อมต่อ เรียก `suggest_connectors`
6. **อัปเดตกำหนดค่า MCP**: เพิ่มกำหนดค่าโดยใช้ `url` จากผลการค้นหา

## การอัปเดตกำหนดค่า MCP ของปลั๊กอิน

### การค้นหาไฟล์กำหนดค่า

1. **ตรวจสอบ `plugin.json`** ว่ามีฟิลด์ `mcpServers` หรือไม่:
   ```json
   {
     "name": "my-plugin",
     "mcpServers": "./config/servers.json"
   }
   ```
   หากมี ให้แก้ไขไฟล์ที่ path นั้น

2. **หากไม่มีฟิลด์ `mcpServers`** ให้ใช้ `.mcp.json` ที่ root ของปลั๊กอิน (ค่าเริ่มต้น)

3. **หาก `mcpServers` ชี้ไปที่ไฟล์ `.mcpb` เท่านั้น** (เซิร์ฟเวอร์ที่ bundled มา) ให้สร้าง `.mcp.json` ใหม่ที่ root ปลั๊กอิน

### รูปแบบไฟล์กำหนดค่า

รองรับทั้งรูปแบบ wrapped และ unwrapped:

```json
{
  "mcpServers": {
    "github": {
      "type": "http",
      "url": "https://api.githubcopilot.com/mcp/"
    }
  }
}
```

ใช้ฟิลด์ `url` จากผลลัพธ์ `search_mcp_registry`

### รายการไดเรกทอรีที่ไม่มี URL

รายการไดเรกทอรีบางรายการไม่มี `url` เนื่องจาก endpoint เป็นแบบ dynamic — ผู้ดูแลระบุเมื่อเชื่อมต่อเซิร์ฟเวอร์ ปลั๊กอินสามารถอ้างอิงเซิร์ฟเวอร์เหล่านี้โดย **ชื่อ** แทน — หากชื่อ MCP เซิร์ฟเวอร์ในกำหนดค่าปลั๊กอินตรงกับชื่อรายการไดเรกทอรี จะถือว่าเหมือนกับการจับคู่ URL
