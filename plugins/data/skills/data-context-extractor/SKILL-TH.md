# Data Context Extractor - สร้าง Data Analysis Skills แบบ Custom

**Type**: User-invoked (slash command)

**Trigger**:
- Bootstrap: "Create a data context skill", "Set up data analysis for our warehouse"
- Iteration: "Add context about [domain]", "Update the data skill with [topic]"

## ภาพรวม

This is a **meta-skill** that creates other skills. มันช่วยให้ Claude เข้าใจ data warehouse, terminology, metrics definitions และ query patterns เฉพาะขององค์กรของคุณ โดยการสอบถามและจดทำ reference files

## ฟีเจอร์หลัก

### Bootstrap Mode (สร้างใหม่)
- ค้นพบ schema ของ data warehouse
- ถามคำถาม key เกี่ยวกับ entities, metrics, data quality issues
- สร้าง skill ที่สมบูรณ์พร้อม reference files:
  - entities.md (entity definitions)
  - metrics.md (KPI calculations)
  - tables/ (domain-specific documentation)

### Iteration Mode (ปรับปรุง)
- โหลด existing skill
- เพิ่มบริบทสำหรับ domain ใหม่
- อัปเดต reference files
- เก็บประวัติการเปลี่ยนแปลง

## Output Format

```
[company]-data-analyst/
├── SKILL.md
└── references/
    ├── entities.md
    ├── metrics.md
    ├── tables/
    │   ├── domain1.md
    │   └── domain2.md
    └── dashboards.json (optional)
```

## การเชื่อมต่อ Inter-Skill

- สร้าง skills ใหม่ที่ซิงค์กับ `analyze`, `write-query`, `explore-data` skills
- ช่วย Claude ใช้ `sql-queries` skill ได้ดีขึ้นด้วยความรู้เฉพาะเจาะจง

## Connector Hints

- `~~data warehouse`: ต้องเชื่อมต่อเพื่อ discover schema และ explore tables
- รองรับ Snowflake, BigQuery, PostgreSQL, Databricks ฯลฯ
