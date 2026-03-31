# /validate-data - QA การวิเคราะห์

**Type**: User-invoked (slash command)

**Trigger**: `/validate-data <การวิเคราะห์ที่ต้องการ review>`

## ภาพรวม

Skill นี้ validate analyses ก่อนนำเสนอต่อ stakeholders โดยตรวจสอบ methodology, accuracy, biases และ potential pitfalls

## ฟีเจอร์หลัก

### Pre-Delivery QA Checklist
- Data quality checks (source verification, freshness, completeness)
- Calculation checks (aggregation logic, denominator correctness)
- Reasonableness checks (magnitude, trend continuity)
- Presentation checks (chart accuracy, number formatting)

### Analytical Pitfall Detection
- Join explosion (many-to-many joins inflating counts)
- Survivorship bias (missing churned users)
- Incomplete period comparison (partial vs full periods)
- Denominator shifting (changing definitions)
- Average of averages (weighted aggregation errors)
- Timezone mismatches
- Selection bias ในการ segment

### Validation Checks
- Spot-check calculations
- Cross-validate with known benchmarks
- Verify subtotals sum correctly
- Check chart axes และ scales

### Confidence Assessment
- **Ready to share**: Methodologically sound, no blocking issues
- **Share with caveats**: Correct but has specific limitations
- **Needs revision**: Found errors or missing analyses

## รูปแบบผลลัพธ์

```
## Validation Report

### Overall Assessment
[Ready to share | Share with caveats | Needs revision]

### Methodology Review
[Findings about approach]

### Issues Found
1. [Severity] [Issue and impact]

### Calculation Spot-Checks
[Verified metrics]

### Required Caveats
[Caveats that must be communicated]
```

## การเชื่อมต่อ Inter-Skill

- มักใช้หลังจาก `/analyze` หรือ `/explore-data`
- อาจต้องใช้ `statistical-analysis` เพื่อ verify statistical claims

## Connector Hints

- อาจต้องเชื่อมต่อ `~~data warehouse` เพื่อ spot-check queries
