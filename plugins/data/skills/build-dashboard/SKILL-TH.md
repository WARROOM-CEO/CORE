# /build-dashboard - สร้าง Interactive Dashboards

**Type**: User-invoked (slash command)

**Trigger**: `/build-dashboard <คำอธิบาย dashboard> [แหล่งข้อมูล]`

## ภาพรวม

Skill นี้สร้าง interactive HTML dashboard ที่สมบูรณ์เหมือนหนึ่งไฟล์ พร้อม charts, filters, KPI cards และ data tables ไม่ต้องการ server หรือ dependencies เฉพาะเปิดในเบราว์เซอร์ได้เลย

## ฟีเจอร์หลัก

- **KPI Cards**: แสดง headline metrics พร้อมการเปลี่ยนแปลงเทียบกับช่วงเวลาก่อนหน้า
- **Interactive Charts**: ใช้ Chart.js สำหรับ line, bar, doughnut, stacked charts
- **Dropdown Filters**: กรองข้อมูลตามมิติต่างๆ (region, product, date range ฯลฯ)
- **Sortable Data Tables**: ดูรายละเอียด data พร้อมฟังก์ชันเรียงลำดับ
- **Professional Styling**: ออกแบบสวยงาม, responsive, สามารถ print ได้

## รูปแบบผลลัพธ์

- Self-contained HTML file ที่สามารถแชร์ได้ทั่วไป
- ไม่ต้อง server — ทำงานแบบ offline เต็มที่
- ข้อมูลทั้งหมดอยู่ใน file เดียว (embedded as JSON)

## Layout Pattern

```
┌──────────────────────────────────────────┐
│ Title                    [Filters ▼]     │
├─────┬─────┬──────┬──────┬──────┬────────┤
│KPI 1│KPI 2│KPI 3 │KPI 4 │KPI 5 │KPI 6  │
├─────┴──────────────────────────┴────────┤
│  Primary Chart       │  Secondary Chart  │
│  (largest area)      │                   │
├─────────────────────┬──────────────────┤
│  Data Table (sortable, scrollable)      │
└─────────────────────┴──────────────────┘
```

## การเชื่อมต่อ Inter-Skill

- ใช้ `sql-queries` skill สำหรับ query ข้อมูลหากเชื่อมต่อ data warehouse
- ใช้ `data-visualization` skill สำหรับเลือก chart type ที่เหมาะสม

## Connector Hints

- `~~data warehouse`: query ข้อมูล live จากตัวเลือกเช่น Snowflake, BigQuery ฯลฯ
- ถ้าไม่มี data warehouse ให้ paste data หรือ upload CSV/Excel
