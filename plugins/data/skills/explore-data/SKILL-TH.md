# /explore-data - Profile และ Explore Dataset

**Type**: User-invoked (slash command)

**Trigger**: `/explore-data <ชื่อตาราง หรือ ไฟล์>`

## ภาพรวม

Skill นี้ให้ profiling ครอบคลุมสำหรับตารางหรือไฟล์ข้อมูล ช่วยให้เข้าใจ shape, quality, patterns ก่อนเริ่มวิเคราะห์

## ฟีเจอร์หลัก

### Data Profiling
- Row count, column count, data types
- Null rates, distinct counts per column
- Percentiles และ distributions
- Min/max values, edge cases

### Quality Assessment
- High null rate detection
- Suspicious values (negative amounts, future dates ฯลฯ)
- Duplicate detection
- Encoding issues (mixed case, whitespace)

### Pattern Discovery
- Natural segments (clustering)
- Correlations between metrics
- Temporal patterns (trends, seasonality)
- Potential join keys และ foreign keys

### Recommendations
- Suggested dimensions ที่ดี (3-50 distinct values)
- Key metrics สำหรับการวิเคราะห์
- Follow-up analyses ที่น่าสนใจ

## รูปแบบผลลัพธ์

```
## Data Profile: [table_name]

### Overview
- Rows: X
- Columns: Y (Z dimensions, W metrics, V dates)
- Date range: [start] to [end]

### Column Details
[summary table with null rates, cardinality, distributions]

### Data Quality Issues
[flagged issues with severity: High/Medium/Low]

### Recommended Explorations
[3-5 specific analyses to run next]
```

## การเชื่อมต่อ Inter-Skill

- ผล exploraton มักนำไปใช้ `/analyze` หรือ `/write-query` ต่อไป
- ใช้ `statistical-analysis` skill สำหรับเจาะลึก patterns

## Connector Hints

- `~~data warehouse`: query profile data จาก live tables
- หรือ upload CSV/Excel file สำหรับ analysis ขนาดเล็กไปกลาง
