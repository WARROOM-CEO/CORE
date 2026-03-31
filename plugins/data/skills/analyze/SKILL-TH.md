# /analyze - ตอบคำถามด้านข้อมูล

**Type**: User-invoked (slash command)

**Trigger**: `/analyze <คำถาม>`

## ภาพรวม

Skill นี้ช่วยตอบคำถามเกี่ยวกับข้อมูล ตั้งแต่การค้นหา metric เดี่ยวอย่างง่ายจนถึงการวิเคราะห์เต็มรูปแบบ และการจัดทำรายงานข้อมูลฟอร์มัล สำหรับ stakeholders

## ฟีเจอร์หลัก

- **การค้นหา Quick Answer**: ค้นหา metric เดี่ยวหรือ lookup ข้อมูลพื้นฐาน เช่น "ผู้ใช้ใหม่ที่ลงทะเบียนเดือนที่แล้วมีกี่คน?"
- **Full Analysis**: ศึกษา trend, drop, หรือความแตกต่างระหว่าง segments พร้อมการเปรียบเทียบแบบตัดสิน
- **Formal Reports**: รายงานครอบคลุมพร้อมวิธีการ, ข้อจำกัด, และคำแนะนำ
- **Validation**: ตรวจสอบผลลัพธ์ก่อนนำเสนอ เพื่อให้มั่นใจว่าข้อมูลถูกต้อง

## รูปแบบผลลัพธ์

- **Quick answer**: คำตอบตรงไปตรงมาพร้อมบริบท และ SQL query ที่ใช้
- **Full analysis**: Findings หลักพร้อม tables และ visualizations, methodology, caveats
- **Formal report**: Executive summary, detailed findings, data quality notes, recommendations

## การเชื่อมต่อ Inter-Skill

- ใช้ `data-visualization` skill เพื่อสร้างกราฟสนับสนุน findings
- ใช้ `statistical-analysis` skill สำหรับการวิเคราะห์ที่ลึกซึ้ง
- ใช้ `validate-data` skill เพื่อ QA ผลลัพธ์ก่อนแชร์

## Connector Hints

ตอนนี้ต้องเชื่อมต่อ `~~data warehouse` เพื่อ query ข้อมูลโดยตรง หากไม่มี คุณสามารถ paste SQL results หรือ upload CSV/Excel file
