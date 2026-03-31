# Data Plugin - ปลั๊กอิน Data Analysis

Data plugin ประกอบด้วยเครื่องมือสำหรับเขียน SQL, explore datasets, สร้าง insights, build visualizations, สร้าง interactive dashboards และ validate analyses ก่อนแชร์ให้ stakeholders ทำงานได้กับ data warehouse ใดๆ, SQL dialect ใดๆ และ analytics stack ใดๆ

## ภาพรวมการทำงาน

Plugin นี้เปลี่ยน Claude ให้เป็น data analyst collaborator ได้ด้วยการเชื่อมต่อ data warehouse MCP server (เช่น Snowflake, Databricks, BigQuery หรือ SQL database ใดๆ) Claude จะสามารถ:

- **Query data warehouse โดยตรง** — explore schemas, run queries, analyze results ทั้งหมด end-to-end
- **Explore and profile** — เข้าใจ data shape, quality, patterns ก่อนวิเคราะห์
- **Write optimized SQL** — เขียน queries ที่ efficient สำหรับ dialect ของคุณ พร้อม best practices
- **Create visualizations** — แปลง data เป็น publication-quality charts ด้วย Python
- **Build dashboards** — สร้าง interactive HTML dashboards ด้วย charts, filters, KPI cards
- **Validate analyses** — QA findings ก่อนนำเสนอ, ตรวจสอบ methodology, accuracy, biases

ถ้าไม่มี data warehouse connection ก็สามารถ paste SQL results, upload CSV/Excel files และ Claude จะสามารถเขียน queries, analyze data, สร้าง visualizations ได้เหมือนกัน

## Skills ทั้งหมด

| Skill | ประเภท | Trigger | เชื่อมโยงกับ |
|-------|--------|---------|-----------|
| analyze | User-invoked | `/analyze <คำถาม>` | data-visualization, statistical-analysis, validate-data |
| explore-data | User-invoked | `/explore-data <ตาราง>` | analyze, write-query |
| write-query | User-invoked | `/write-query <คำอธิบาย>` | sql-queries, analyze, create-viz |
| create-viz | User-invoked | `/create-viz <ข้อมูล>` | data-visualization, statistical-analysis |
| build-dashboard | User-invoked | `/build-dashboard <คำอธิบาย>` | data-visualization, write-query |
| validate-data | User-invoked | `/validate-data <analysis>` | (validation skill) |
| data-context-extractor | User-invoked | Bootstrap/Iteration triggers | (meta-skill สำหรับสร้าง custom skills) |
| data-visualization | Model-invoked | (auto-triggered) | (chart patterns, design principles) |
| sql-queries | Model-invoked | (auto-triggered) | (SQL reference, dialects) |
| statistical-analysis | Model-invoked | (auto-triggered) | (statistical methods, trend analysis) |

### คำอธิบาย Skill ที่ User-Invoked

**analyze**: ตอบคำถามด้านข้อมูล ตั้งแต่การ lookup metric เดี่ยวไปถึงการวิเคราะห์เต็มรูปแบบ ใช้เมื่อต้องการ lookup metric, สืบสวน trend หรือ drop, เปรียบเทียบ segments หรือเตรียมรายงานข้อมูลสำหรับ stakeholders

**explore-data**: Profile และ explore dataset เพื่อทำความเข้าใจ shape, quality และ patterns ใช้เมื่อพบตารางหรือไฟล์ใหม่, ตรวจสอบ null rates และ distributions, หา data quality issues หรือตัดสินใจว่าจะวิเคราะห์ dimension และ metric ไหน

**write-query**: เขียน SQL ที่ optimize แล้วสำหรับ dialect ของคุณพร้อม best practices ใช้เมื่อแปลง natural-language data need เป็น SQL, สร้าง multi-CTE query พร้อม joins, optimize query บนตารางขนาดใหญ่ หรือต้องการ dialect-specific syntax

**create-viz**: สร้าง visualizations คุณภาพสูงด้วย Python ใช้เมื่อแปลง query results หรือ DataFrame เป็น chart, เลือก chart type ที่เหมาะสม หรือต้องการ interactive chart พร้อม hover และ zoom

**build-dashboard**: สร้าง interactive HTML dashboard พร้อม charts, filters และตาราง ใช้เมื่อต้องการ executive overview พร้อม KPI cards, แปลง query results เป็น shareable report หรือสร้าง monitoring snapshot

**validate-data**: QA การวิเคราะห์ก่อนแชร์ — ตรวจสอบ methodology, accuracy และ bias ใช้เมื่อ review การวิเคราะห์ก่อน stakeholder presentation, ตรวจสอบ calculations, ยืนยัน SQL results หรือประเมินว่า conclusions มีหลักฐานรองรับจริงไหม

**data-context-extractor**: สร้างหรือปรับปรุง company-specific data analysis skill โดยดึงความรู้จาก analysts ใช้ 2 modes:
- **Bootstrap**: สร้าง skill ใหม่จาก scratch สำหรับ data warehouse ของคุณ
- **Iteration**: ปรับปรุง existing skill โดยเพิ่ม domain-specific context

## โครงสร้างไฟล์

| English File | Thai File | วัตถุประสงค์ |
|--------------|-----------|-----------|
| `plugin.json` | — | Metadata + description |
| `CONNECTORS.md` | `CONNECTORS-TH.md` | Tool categories, MCP references |
| `README.md` | — (This file in Thai) | Plugin overview ภาษาไทย |
| `skills/analyze/SKILL.md` | `skills/analyze/SKILL-TH.md` | Skill description + user guide |
| `skills/build-dashboard/SKILL.md` | `skills/build-dashboard/SKILL-TH.md` | Dashboard building patterns, templates |
| `skills/create-viz/SKILL.md` | `skills/create-viz/SKILL-TH.md` | Visualization patterns, chart selection |
| `skills/data-context-extractor/SKILL.md` | `skills/data-context-extractor/SKILL-TH.md` | Meta-skill for creating custom skills |
| `skills/explore-data/SKILL.md` | `skills/explore-data/SKILL-TH.md` | Data profiling patterns, quality framework |
| `skills/validate-data/SKILL.md` | `skills/validate-data/SKILL-TH.md` | QA patterns, pitfall detection |
| `skills/write-query/SKILL.md` | `skills/write-query/SKILL-TH.md` | Query optimization patterns |
| `skills/data-visualization/SKILL.md` | — | Chart selection, design principles (model-invoked) |
| `skills/sql-queries/SKILL.md` | — | SQL reference by dialect (model-invoked) |
| `skills/statistical-analysis/SKILL.md` | — | Statistical methods reference (model-invoked) |

### Bilingual Design Pattern

ไฟล์หลัก (SKILL.md) มี Thai description ในประเด็น frontmatter และ language directive อธิบายว่า user-facing output ต้องเป็น Thai ส่วน internal logic, code, technical values ยังคงเป็น English

ไฟล์ SKILL-TH.md เป็น Thai user-facing summary ของแต่ละ skill รวม trigger, features, output format, inter-skill connections, connector hints

## สัญญาอนุญาต

ปลั๊กอินนี้ใช้ Apache 2.0 License

| สิทธิ | Apache 2.0 |
|------|-----------|
| Use commercially | ✅ |
| Modify code | ✅ |
| Distribute modified | ✅ |
| Private use | ✅ |
| Place liability | ❌ |
| Place warranty | ❌ |
| Require license notification | ✅ |
