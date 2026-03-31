# /ticket-triage

ทักษะ Triage และจัดลำดับความสำคัญ support ticket หรือปัญหาของ customer

**ประเภท:** User-invoked
**Trigger:** `/ticket-triage <ticket or issue description>`

## ภาพรวม

ใช้ skill นี้เพื่อจัดหมวดหมู่ (categorize) และจัดลำดับความสำคัญ (prioritize) support ticket ใหม่ ผลลัพธ์คือ structured triage assessment พร้อมคำแนะนำในการส่งต่อและ draft response แรกถึง customer

## ใช้เมื่อ

- Ticket ใหม่เข้ามาและต้องการ categorization
- ต้องการกำหนด priority P1-P4 สำหรับ ticket
- ต้องตัดสินใจว่าทีมไหนควร handle ticket นี้
- ต้องการตรวจสอบว่า ticket นี้เป็น duplicate หรือเป็น known issue

## ผลลัพธ์หลัก

**Structured Triage Assessment** ประกอบด้วย:
- Issue summary (สรุปปัญหา)
- Category (Bug, Feature Request, Billing, Account, How-to, Integration, Security, Data, Performance)
- Priority P1-P4 พร้อมเหตุผล
- Product area ที่เกี่ยวข้อง
- Routing recommendation (ทีมไหนควร handle)
- Key details (customer context, impact, workaround status)
- Suggested initial response ถึง customer
- Internal notes สำหรับเจ้าหน้าที่

## ลำดับความสำคัญ (Priority Levels)

| Priority | ความหมาย | SLA Response | สถานการณ์ |
|----------|---------|-------------|---------|
| **P1** | Critical | 1 hour | Production down, data loss, security breach, ผู้ใช้ส่วนใหญ่ได้รับผลกระทบ |
| **P2** | High | 4 hours | Core workflow broken, multiple users affected, no workaround |
| **P3** | Medium | 1 business day | Feature partial broken, workaround available, single user/small team |
| **P4** | Low | 2 business days | Cosmetic issue, feature request, general question |

## หมวดหมู่ (Categories)

- **Bug** — Product ทำงานผิด (Error, broken, crash, not working)
- **How-to** — Customer ต้องการคำแนะนำการใช้ (How do I, setting up, configure)
- **Feature request** — Customer ขอความสามารถใหม่ (Would be great if, any plans to)
- **Billing** — Payment, subscription, refund issues
- **Account** — Login, password, access, permission issues
- **Integration** — API, webhook, third-party tool connection issues
- **Security** — Data breach, compliance, vulnerability concerns
- **Data** — Missing data, import/export, migration issues
- **Performance** — Slow, timeout, unavailable, degraded service

## Routing Recommendations

| Route to | เมื่อ |
|----------|------|
| **Tier 1** | How-to questions, known issues, billing inquiries, password resets |
| **Tier 2** | Bugs requiring investigation, complex configuration, integration troubleshooting |
| **Engineering** | Confirmed bugs, infrastructure issues, performance degradation |
| **Product** | Feature requests with demand, design decisions, workflow gaps |
| **Security** | Data access concerns, vulnerability reports, compliance questions |
| **Billing** | Refund requests, contract disputes, complex billing adjustments |

## เชื่อมโยงกับ

- `/draft-response` — เมื่อต้องการ draft full response ถึง customer
- `/customer-research` — เมื่อต้องการค้นคว้าข้อมูล context เพิ่มเติม
- `/customer-escalation` — เมื่อ ticket ต้องการ escalation ถึง engineering/product/leadership
