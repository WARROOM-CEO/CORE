# /kb-article

ทักษะร่าง knowledge base article จาก resolved issue หรือคำถามที่พบบ่อย

**ประเภท:** User-invoked
**Trigger:** `/kb-article <resolved issue or ticket>`

## ภาพรวม

ใช้ skill นี้เพื่อร่าง publish-ready knowledge base article จาก resolved support issue, common question, หรือ documented workaround ผลลัพธ์คือ article ที่ structured สำหรับ searchability และ self-service

## ใช้เมื่อ

- Ticket resolution คุ้มค่าต่อการ document สำหรับ self-service
- คำถามเดิมปรากฏซ้ำกับหลาย customers
- Workaround ต้องการ publish ให้ customers
- Known issue ควร communicate ให้เป็นทางการ
- Product change ต้อง document step-by-step

## ผลลัพธ์หลัก

**KB Article Draft** ประกอบด้วย:
- Title (searchable, describes outcome or problem)
- Overview (1-2 sentences, explains scope and audience)
- Article body (structured per type: How-to/Troubleshooting/FAQ/Known Issue/Reference)
- Related articles (links to companion content)
- Metadata (category, tags, audience, last updated)
- Publishing notes (source, existing articles to update, review needed from, suggested review date)

## Article Types

### How-to Articles
**วัตถุประสงค์:** Step-by-step instructions for accomplishing a task
**โครงสร้าง:** Prerequisites → Steps → Verify It Worked → Common Issues → Related Articles

### Troubleshooting Articles
**วัตถุประสงค์:** Diagnose and resolve specific problem
**โครงสร้าง:** Symptoms → Cause → Solution Options → Prevention → Still Having Issues?

### FAQ Articles
**วัตถุประสงค์:** Quick answer to common question
**โครงสร้าง:** Question → Direct Answer → Details → Related Questions

### Known Issue Articles
**วัตถุประสงค์:** Document known bug or limitation with workaround
**โครงสร้าง:** Status → Affected → Symptoms → Workaround → Fix Timeline → Updates

### Reference Articles
**วัตถุประสงค์:** Reference material (pricing, features, technical specs)
**โครงสร้าง:** Overview → Detailed Reference → Tables/Lists → Related Articles

## Searchability Best Practices

**ชื่อที่ดี:**
- "How to configure SSO with Okta" (specific, includes tool name)
- "Fix: Dashboard shows blank page" (includes symptom)
- "Error: 'Connection refused' when importing data" (includes exact error message)

**Keyword Optimization:**
- Include exact error messages (customers copy-paste into search)
- Use customer language, not internal jargon ("can't log in" not "authentication failure")
- Include common synonyms ("delete/remove", "export/download")
- Add alternate phrasings for different search angles
- Tag with product areas matching customer thinking

**Opening Sentence Formula:**
- How-to: "This guide shows you how to [accomplish X]."
- Troubleshooting: "If you're seeing [symptom], this article explains how to fix it."
- FAQ: "[Question]? Here's the answer."
- Known issue: "Some users are experiencing [symptom]. Here's what we know."

## Formatting Standards

- Use headers (H2, H3) to break content into scannable sections
- Use numbered lists for sequential steps
- Use bullet lists for non-sequential items
- Use bold for UI element names and key terms
- Use code blocks for commands, API calls, error messages
- Use tables for comparisons and reference data
- Use callouts for warnings, tips, important caveats
- Keep paragraphs short (2-4 sentences max)
- One idea per section

## When to Update vs. Create New

**Update existing** when:
- Product changed, steps need refreshing
- Article mostly right but missing detail
- Feedback shows customer confusion
- Better workaround found

**Create new** when:
- New feature/product area needs documentation
- Resolved ticket reveals gap
- Existing article too broad, should be split
- Different audience needs different explanation

## Review and Maintenance Cadence

| Activity | Frequency | Who |
|----------|-----------|-----|
| New article review | Before publishing | Peer + SME for technical |
| Accuracy audit | Quarterly | Support team |
| Stale content check | Monthly | Flag articles not updated in 6+ months |
| Known issue updates | Weekly | Update status on open issues |
| Analytics review | Monthly | Check traffic and helpfulness ratings |
| Gap analysis | Quarterly | Identify top ticket topics without KB articles |

## Category Taxonomy

```
Getting Started
├── Account setup
├── First-time configuration
└── Quick start guides

Features & How-tos
├── [Feature area 1]
├── [Feature area 2]
└── [Feature area 3]

Integrations
├── [Integration 1]
├── [Integration 2]
└── API reference

Troubleshooting
├── Common errors
├── Performance issues
└── Known issues

Billing & Account
├── Plans and pricing
├── Billing questions
└── Account management
```

## เชื่อมโยงกับ

- `/ticket-triage` — เพื่อ triage ticket ก่อนก่อน convert เป็น KB article
- `/customer-research` — เพื่อ gather background ถ้า article ต้อง verify
- `/draft-response` — เพื่อ draft customer communication about KB article
