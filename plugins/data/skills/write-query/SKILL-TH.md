# /write-query - เขียน SQL ที่ Optimized

**Type**: User-invoked (slash command)

**Trigger**: `/write-query <คำอธิบายข้อมูลที่ต้องการ>`

## ภาพรวม

Skill นี้เขียน SQL queries ที่ optimize แล้ว สำหรับ SQL dialect ที่คุณใช้ (Snowflake, BigQuery, PostgreSQL, Databricks, Redshift, MySQL ฯลฯ) พร้อม best practices

## ฟีเจอร์หลัก

### Query Construction
- Parse natural language description เป็น SQL structure
- Identify output columns, filters, aggregations, joins
- Determine sort order และ limits

### Dialect Support
- PostgreSQL (Aurora, RDS, Supabase)
- Snowflake
- BigQuery
- Redshift
- Databricks SQL
- MySQL
- SQL Server
- DuckDB, SQLite

### Optimization Strategies
- ใช้ CTEs สำหรับ readability
- Filter early (push WHERE clauses)
- Partition filters สำหรับ performance
- Avoid `SELECT *` — specify columns
- Use appropriate JOIN types
- Detect และ prevent exploding joins

### Best Practices
- Readable naming (table aliases ที่มีความหมาย)
- Comments อธิบาย "why" ไม่ใช่แค่ "what"
- Dialect-specific syntax และ performance features

## รูปแบบผลลัพธ์

- Complete query พร้อม syntax highlighting
- Brief explanation ของแต่ละ CTE หรือ section
- Performance notes (partition usage, bottlenecks)
- Modification suggestions เพื่อ variations

## SQL Dialect Examples

```sql
-- Snowflake date arithmetic
DATEADD(day, 7, date_column)

-- BigQuery date arithmetic
DATE_ADD(date_column, INTERVAL 7 DAY)

-- PostgreSQL date arithmetic
date_column + INTERVAL '7 days'
```

## การเชื่อมต่อ Inter-Skill

- ใช้ `sql-queries` skill เพื่อ dialect-specific patterns และ reference
- ผล output มักจะถูกส่งไปยัง `/analyze` หรือ `/create-viz`

## Connector Hints

- `~~data warehouse`: schema discovery และ execution
- หรือให้ table names พร้อม schema details
