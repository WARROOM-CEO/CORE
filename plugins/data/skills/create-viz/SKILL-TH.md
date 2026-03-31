# /create-viz - สร้าง Visualizations

**Type**: User-invoked (slash command)

**Trigger**: `/create-viz <แหล่งข้อมูล> [chart type] [คำแนะนำเพิ่มเติม]`

## ภาพรวม

Skill นี้สร้าง publication-quality visualizations ด้วย Python (matplotlib, seaborn หรือ plotly) เหมาะสำหรับแปลง query results หรือ DataFrame เป็น charts ที่ดูดี

## ฟีเจอร์หลัก

- **Chart Type Recommendation**: เลือก chart type ที่เหมาะสมตามข้อมูล เช่น:
  - Line chart สำหรับ time series
  - Bar chart สำหรับ comparison
  - Scatter plot สำหรับ correlation
  - Heatmap สำหรับ matrix relationships
- **Design Best Practices**: สีสวยงาม, typography ดี, layout สมดุล
- **Accessibility**: สนับสนุน colorblind-friendly palettes, readable fonts
- **Interactive Charts**: สามารถขอ interactive charts พร้อม hover, zoom, legend

## รูปแบบผลลัพธ์

- PNG image file พร้อมคุณภาพสูง (150 dpi)
- Python code ที่สามารถ modify ได้
- Suggestions สำหรับ variations (chart type ต่างๆ, grouping ต่างๆ)

## Chart Selection Guide

| ข้อมูล | Chart Type ที่ดี |
|-------|-----------------|
| Trend over time | Line chart |
| Comparison across categories | Bar chart |
| Part-to-whole | Stacked bar, treemap |
| Distribution | Histogram, box plot |
| Correlation (2 vars) | Scatter plot |
| Geographic | Choropleth map |

## การเชื่อมต่อ Inter-Skill

- ใช้ `sql-queries` skill สำหรับเขียน query ก่อน
- ใช้ `statistical-analysis` skill สำหรับการวิเคราะห์เพิ่มเติม

## Connector Hints

- `~~data warehouse`: query data หากต้อง
- หรือ paste query results โดยตรง
