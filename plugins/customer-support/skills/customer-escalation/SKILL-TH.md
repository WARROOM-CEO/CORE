# /customer-escalation

ทักษะจัดทำ escalation สำหรับ engineering, product, หรือ leadership

**ประเภท:** User-invoked
**Trigger:** `/customer-escalation <issue summary> [customer name]`

## ภาพรวม

ใช้ skill นี้เพื่อ package support issue เป็น structured escalation brief สำหรับ engineering, product, หรือ leadership ผลลัพธ์คือ escalation package ที่มี context ครบถ้วน, reproduction steps, business impact assessment, และ customer communication strategy

## ใช้เมื่อ

- Bug ต้องการความสนใจนอกเหนือ normal support
- Multiple customers รายงานปัญหาเดียวกัน
- Customer กำลังจะ churn หรือคุกคาม escalate ต่อ
- ปัญหาค้างเกิน SLA
- Issue requires code fix, infrastructure investigation, หรือ product decision

## ผลลัพธ์หลัก

**Structured Escalation Brief** ประกอบด้วย:
- One-line summary
- Severity level (Critical/High/Medium)
- Target team (Engineering/Product/Security/Leadership)
- Impact assessment (customers affected, workflow impact, revenue at risk, duration)
- Detailed issue description
- Troubleshooting steps already tried
- Reproduction steps (for bugs)
- Customer communication status
- What's needed (investigate, prioritize fix, make decision, approve exception)
- Supporting context (related tickets, logs, links)

## Severity Levels

| Severity | ความหมาย | SLA |
|----------|---------|-----|
| **Critical** | Production down, data at risk, security breach, multiple high-value customers affected | Immediate attention |
| **High** | Major functionality broken, key customer blocked, SLA at risk | Same-day attention |
| **Medium** | Significant issue with workaround, important but not urgent | This week |

## Escalation Tiers

### L2 → Engineering
**เมื่อ:** Confirmed bug, infrastructure issue, needs code change
**รวมเข้า:** Reproduction steps, environment details, logs, business impact, customer timeline

### L2 → Product
**เมื่อ:** Feature gap, design decision needed, workflow mismatch, competing needs
**รวมเข้า:** Customer use case, business impact, frequency of request, competitive pressure

### Any → Security
**เมื่อ:** Data exposure, unauthorized access, vulnerability, compliance concern
**รวมเข้า:** What was observed, who/what affected, containment steps, urgency

### Any → Leadership
**เมื่อ:** High-revenue customer churn risk, SLA breach, cross-functional decision, policy exception needed
**รวมเข้า:** Full business context, revenue at risk, what's been tried, specific ask, deadline

## Business Impact Assessment

| Dimension | ถามคำถาม |
|-----------|---------|
| **Breadth** | Customers/users affected? Growing? |
| **Depth** | Blocked vs. inconvenienced? |
| **Duration** | How long? Until critical? |
| **Revenue** | ARR at risk? Pending deals affected? |
| **Reputation** | Public risk? Reference customer? |
| **Contractual** | SLA breach? Contract obligations? |

## Reproduction Steps (for bugs)

Best practices:
1. Start from clean state (describe starting point)
2. Be specific ("Click Export button in top-right of Dashboard page")
3. Include exact values (specific inputs, dates, IDs)
4. Note environment (browser, OS, account type, plan level)
5. Capture frequency (always? intermittent? certain conditions?)
6. Include evidence (screenshots, exact error messages, logs)
7. Note what you've ruled out (tested in multiple browsers, etc.)

## Follow-up Cadence After Escalation

| Severity | Internal | Customer |
|----------|----------|----------|
| **Critical** | Every 2 hours | Every 2-4 hours (or per SLA) |
| **High** | Every 4 hours | Every 4-8 hours |
| **Medium** | Daily | Every 1-2 business days |

## เชื่อมโยงกับ

- `/ticket-triage` — เพื่อ triage ticket ก่อน escalate
- `/customer-research` — เพื่อ gather context เพิ่มเติม
- `/draft-response` — เพื่อ draft customer communication เกี่ยวกับ escalation
- `/kb-article` — เมื่อ escalation reveals knowledge gap
