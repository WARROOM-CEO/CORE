# Connectors - การเชื่อมต่อ

## วิธีการใช้เครื่องมือ Reference

ไฟล์ใน plugin ใช้ `~~หมวดหมู่` เป็น placeholder สำหรับเครื่องมือที่คุณเชื่อมต่อในหมวดหมู่นั้น เช่น `~~data warehouse` อาจหมายถึง Snowflake, BigQuery หรือ data warehouse อื่นที่มี MCP server

Plugins มี **tool-agnostic** — พวกเขาบรรยายงาน workflows ในแง่ของหมวดหมู่ (data warehouse, notebook, product analytics ฯลฯ) แทนที่จะเป็น specific products `.mcp.json` pre-configures specific MCP servers แต่ MCP server ใดๆ ในหมวดหมู่นั้นจะทำงาน

## Connectors สำหรับ Plugin นี้

| หมวดหมู่ | Placeholder | Included Servers | ตัวเลือกอื่น |
|---------|-------------|-----------------|------------|
| Data warehouse | `~~data warehouse` | Snowflake\*, Databricks\*, BigQuery, Definite | Redshift, PostgreSQL, MySQL |
| Notebook | `~~notebook` | Hex | Jupyter, Deepnote, Observable |
| Product analytics | `~~product analytics` | Amplitude | Mixpanel, Heap |
| Project tracker | `~~project tracker` | Atlassian (Jira/Confluence) | Linear, Asana |

\* Placeholder — MCP URL ยังไม่ได้กำหนดค่า

## Data Warehouse Connectors

### Data Warehouse Category
เชื่อมต่อเพื่อให้ Claude สามารถ:
- Query data โดยตรง
- Explore schemas และ table metadata
- Run analyses end-to-end โดยไม่ต้อง copy-paste
- Optimize queries สำหรับ performance

**ตัวเลือก**:
- **Snowflake**: Data cloud platform ด้วย clustering, semi-structured data support
- **Databricks**: Lake house analytics พร้อม Delta Lake
- **BigQuery**: Google's serverless data warehouse พร้อม built-in ML
- **Redshift**: Amazon's data warehouse ด้วย columnar storage
- **PostgreSQL**: Open-source relational database (including Aurora, RDS, Supabase)
- **MySQL**: Open-source relational database (including Aurora MySQL, PlanetScale)

### Notebook Category
เชื่อมต่อเพื่อจัดเก็บและแชร์ analyses ที่มี code, visualizations, narrative

**ตัวเลือก**:
- **Hex**: Collaborative data notebooks
- **Jupyter**: Classic notebook environment
- **Deepnote**: Collaborative Jupyter alternative
- **Observable**: Reactive JavaScript notebooks

### Product Analytics Category
เชื่อมต่อเพื่อวิเคราะห์ user behavior, events, funnels

**ตัวเลือก**:
- **Amplitude**: Event analytics platform
- **Mixpanel**: Product analytics
- **Heap**: Automatic event capture

### Project Tracker Category
เชื่อมต่อเพื่อ link data analyses ไปยัง issues, tickets, roadmap items

**ตัวเลือก**:
- **Atlassian** (Jira/Confluence): Issue tracking และ documentation
- **Linear**: Modern issue tracking
- **Asana**: Project management
