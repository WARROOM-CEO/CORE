# /draft-response

ทักษะร่าง response ที่เป็นมืออาชีพสำหรับ customer

**ประเภท:** User-invoked
**Trigger:** `/draft-response <situation description>`

## ภาพรวม

ใช้ skill นี้เพื่อร่าง professional, customer-facing response ที่ tailored ตามสถานการณ์ และความสัมพันธ์กับ customer ผลลัพธ์คือ draft response พร้อมกับ tone guidance, internal notes, risk assessment, และคำแนะนำ

## ใช้เมื่อ

- ตอบคำถาม product
- Respond ต่อ escalation หรือ outage
- แจ้งข่าวไม่ดี (delay, won't-fix, billing error)
- ปฏิเสธ feature request
- ส่งข่าวดี (feature launch, recognition)

## ผลลัพธ์หลัก

**Draft Response** ประกอบด้วย:
- Customer contact name
- Subject/topic
- Channel indication (Email/Ticket/Chat)
- Tone specification (Empathetic/Professional/Technical/Celebratory/Candid)
- Full draft response text
- Internal notes (tone rationale, verification needed, risk factors, follow-up actions)

## Tone Guidance

| สถานการณ์ | Tone | เจตนา |
|----------|------|------|
| **Good news** | Celebratory | Enthusiastic, warm, congratulatory |
| **Routine update** | Professional | Clear, concise, friendly |
| **Technical** | Precise | Accurate, detailed, structured |
| **Delayed delivery** | Accountable | Honest, apologetic, action-oriented |
| **Bad news** | Candid | Direct, empathetic, solution-oriented |
| **Issue/outage** | Urgent | Immediate, transparent, reassuring |
| **Escalation** | Executive | Composed, ownership-taking, confident |
| **Billing** | Precise | Clear, factual, empathetic, solution-focused |

## Situation Types & Approaches

**Answering Product Question:**
- Lead with direct answer
- Provide relevant documentation links
- Offer further help if needed

**Bug/Issue Response:**
- Acknowledge impact on their work
- State what you know about status
- Provide workaround if available
- Set expectations for timeline

**Handling Escalation:**
- Acknowledge severity and frustration
- Take ownership, no deflecting
- Provide clear action plan with timeline
- Identify accountable person

**Delivering Bad News:**
- Be direct, don't bury the news
- Explain reasoning honestly
- Acknowledge specific impact on them
- Offer alternatives or mitigation

**Declining Request:**
- Acknowledge the request and reasoning
- Be honest about decision
- Explain why without dismissing
- Offer alternatives when possible

## Response Structure Best Practices

1. **Acknowledgment** (1-2 sentences) — Show you understand their situation
2. **Core Message** (1-3 paragraphs) — Deliver main info, be specific
3. **Next Steps** (1-3 bullets) — What you'll do, what they do, when they'll hear back
4. **Closing** (1 sentence) — Warm, professional sign-off

## Length Guidelines

| Channel | ความยาว |
|---------|--------|
| Chat/IM | 1-4 sentences |
| Support ticket | 1-3 short paragraphs |
| Email | 3-5 paragraphs max |
| Escalation | As needed, well-structured |
| Executive | 2-3 paragraphs max |

## เชื่อมโยงกับ

- `/ticket-triage` — เมื่อต้องการ triage ticket ก่อน draft response
- `/customer-research` — เมื่อต้องการ context จาก research sources
- `/customer-escalation` — เมื่อต้อง escalate issue พร้อมกับ customer communication
- `/kb-article` — เมื่อ response insights ควร document เป็น KB article
