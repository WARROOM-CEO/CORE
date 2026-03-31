# JSON Schemas — ฉบับภาษาไทย

เอกสารนี้อธิบาย JSON schemas ทั้งหมดที่ skill-creator ใช้งาน

---

## evals.json

กำหนด eval cases สำหรับ Skill อยู่ที่ `evals/evals.json` ใน Skill directory

```json
{
  "skill_name": "example-skill",
  "evals": [
    {
      "id": 1,
      "prompt": "prompt ของผู้ใช้",
      "expected_output": "คำอธิบายผลลัพธ์ที่คาดหวัง",
      "files": ["evals/files/sample1.pdf"],
      "expectations": [
        "output มี X",
        "skill ใช้ script Y"
      ]
    }
  ]
}
```

| Field | รายละเอียด |
|-------|-----------|
| `skill_name` | ชื่อตรงกับ frontmatter ของ Skill |
| `evals[].id` | ตัวเลข identifier ที่ไม่ซ้ำกัน |
| `evals[].prompt` | task ที่ต้องการให้ execute |
| `evals[].expected_output` | คำอธิบาย success สำหรับมนุษย์อ่าน |
| `evals[].files` | รายการ input files (optional, relative path) |
| `evals[].expectations` | รายการ assertions ที่ตรวจสอบได้ |

---

## grading.json

ผลลัพธ์จาก Grader Agent อยู่ที่ `<run-dir>/grading.json`

```json
{
  "expectations": [
    {
      "text": "output มีชื่อ 'สมชาย ใจดี'",
      "passed": true,
      "evidence": "พบใน transcript ขั้นที่ 3: 'สกัดชื่อ: สมชาย ใจดี'"
    }
  ],
  "summary": {
    "passed": 2,
    "failed": 1,
    "total": 3,
    "pass_rate": 0.67
  },
  "execution_metrics": {
    "tool_calls": { "Read": 5, "Write": 2, "Bash": 8 },
    "total_tool_calls": 15,
    "total_steps": 6,
    "errors_encountered": 0,
    "output_chars": 12450,
    "transcript_chars": 3200
  },
  "timing": {
    "executor_duration_seconds": 165.0,
    "grader_duration_seconds": 26.0,
    "total_duration_seconds": 191.0
  },
  "claims": [
    {
      "claim": "ฟอร์มมี 12 ช่องกรอก",
      "type": "factual",
      "verified": true,
      "evidence": "นับจาก field_info.json ได้ 12 ช่อง"
    }
  ],
  "eval_feedback": {
    "suggestions": [{ "assertion": "...", "reason": "..." }],
    "overall": "ข้อสังเกตโดยรวม"
  }
}
```

**ชื่อ field ที่สำคัญ:** Viewer ใช้ `text`, `passed`, `evidence` — ห้ามใช้ชื่ออื่นเช่น `name`/`met`/`details`

---

## benchmark.json

ผลลัพธ์จาก Benchmark mode อยู่ที่ `<workspace>/iteration-N/benchmark.json`

```json
{
  "metadata": {
    "skill_name": "pdf",
    "timestamp": "2026-01-15T10:30:00Z",
    "evals_run": [1, 2, 3],
    "runs_per_configuration": 3
  },
  "runs": [
    {
      "eval_id": 1,
      "eval_name": "Ocean",
      "configuration": "with_skill",
      "run_number": 1,
      "result": {
        "pass_rate": 0.85,
        "passed": 6,
        "failed": 1,
        "total": 7,
        "time_seconds": 42.5,
        "tokens": 3800,
        "errors": 0
      }
    }
  ],
  "run_summary": {
    "with_skill": {
      "pass_rate": { "mean": 0.85, "stddev": 0.05 },
      "time_seconds": { "mean": 45.0, "stddev": 12.0 },
      "tokens": { "mean": 3800, "stddev": 400 }
    },
    "without_skill": {
      "pass_rate": { "mean": 0.35, "stddev": 0.08 }
    },
    "delta": { "pass_rate": "+0.50", "time_seconds": "+13.0" }
  },
  "notes": ["สังเกต pattern ที่น่าสนใจ..."]
}
```

**ข้อสำคัญ:** Viewer ใช้ field name เหล่านี้ตรงๆ — ใช้ `configuration` ไม่ใช่ `config`, วาง `pass_rate` ใน `result` ไม่ใช่ top level

---

## comparison.json

ผลลัพธ์จาก Blind Comparator อยู่ที่ `<grading-dir>/comparison.json`

```json
{
  "winner": "A",
  "reasoning": "เหตุผลที่เลือก A",
  "rubric": {
    "A": { "content_score": 4.7, "structure_score": 4.3, "overall_score": 9.0 },
    "B": { "content_score": 2.7, "structure_score": 2.7, "overall_score": 5.4 }
  },
  "output_quality": {
    "A": { "score": 9, "strengths": ["..."], "weaknesses": ["..."] },
    "B": { "score": 5, "strengths": ["..."], "weaknesses": ["..."] }
  }
}
```

---

## analysis.json

ผลลัพธ์จาก Post-hoc Analyzer อยู่ที่ `<grading-dir>/analysis.json`

```json
{
  "comparison_summary": {
    "winner": "A",
    "winner_skill": "path/to/skill",
    "loser_skill": "path/to/skill",
    "comparator_reasoning": "สรุปเหตุผล"
  },
  "winner_strengths": ["..."],
  "loser_weaknesses": ["..."],
  "instruction_following": {
    "winner": { "score": 9, "issues": ["..."] },
    "loser": { "score": 6, "issues": ["..."] }
  },
  "improvement_suggestions": [
    {
      "priority": "high",
      "category": "instructions",
      "suggestion": "คำแนะนำที่เป็น action ได้",
      "expected_impact": "ผลที่คาดว่าจะเกิดขึ้น"
    }
  ]
}
```

---

## timing.json

ข้อมูลเวลาของแต่ละ run อยู่ที่ `<run-dir>/timing.json`

**วิธีเก็บ:** เมื่อ subagent task เสร็จ notification จะมี `total_tokens` และ `duration_ms` — บันทึกทันที ข้อมูลนี้ไม่ถูกเก็บที่อื่น

```json
{
  "total_tokens": 84852,
  "duration_ms": 23332,
  "total_duration_seconds": 23.3,
  "executor_duration_seconds": 165.0,
  "grader_duration_seconds": 26.0
}
```

---

## metrics.json

ข้อมูล execution metrics จาก executor อยู่ที่ `<run-dir>/outputs/metrics.json`

```json
{
  "tool_calls": { "Read": 5, "Write": 2, "Bash": 8 },
  "total_tool_calls": 18,
  "total_steps": 6,
  "files_created": ["output.pdf"],
  "errors_encountered": 0,
  "output_chars": 12450,
  "transcript_chars": 3200
}
```
