# DSS Conference 2026: Agent-First Submission Guide

## Purpose

DSS is piloting an agent-first submission intake for talks and workshops.
This page is the single submission spec.

Read it with:

```bash
curl -fsSL https://dss-submit-test.github.io/submit.md
```

## Scope

- Conference: DeFi Security Summit (DSS) 2026
- Submission types:
  - `lightning` (5 min)
  - `talk` (20 min)
  - `panel` (45 min)
  - `workshop` (60 min)
- Review model for this prototype:
  - structured intake
  - agent pre-screen
  - human committee final decision
- Next phase:
  - double-blind reviewer workflow

## Step 1: Register

Create your registration payload (`registration.json`):

```json
{
  "registrant_id": "reg_example_001",
  "full_name": "Your Name",
  "email": "you@example.com",
  "organization": "Your Org",
  "role": "Security Researcher",
  "telegram_or_x": "@handle",
  "country": "US"
}
```

Required fields:

- `registrant_id`
- `full_name`
- `email`
- `organization`
- `role`

## Step 2: Prepare Submission

Create your submission payload (`submission.json`):

```json
{
  "submission_id": "sub_example_001",
  "registrant_id": "reg_example_001",
  "session_type": "talk",
  "title": "Your Session Title",
  "abstract": "One clear paragraph describing the technical content and practical value.",
  "audience_level": "advanced",
  "preferred_duration_minutes": 20,
  "key_takeaways_csv": "Item 1,Item 2,Item 3",
  "evidence_links_csv": "https://github.com/org/repo,https://docs.google.com/presentation/..."
}
```

Required fields:

- `submission_id`
- `registrant_id`
- `session_type`
- `title`
- `abstract`
- `audience_level`

## Step 3: Submit to DSS Platform

Webhook endpoint:

```text
https://script.google.com/macros/s/AKfycbypCvYoGHWW7qK9_J3ugGm6xREHxPt9voYnQEeYRcohem5kdYiLhsPxFC-1dFuDenKT/exec
```

Send one combined payload:

```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -d @payload.json \
  "https://script.google.com/macros/s/AKfycbypCvYoGHWW7qK9_J3ugGm6xREHxPt9voYnQEeYRcohem5kdYiLhsPxFC-1dFuDenKT/exec"
```

Where `payload.json` is:

```json
{
  "source": "dss-agent-submit-md",
  "version": "0.1",
  "submitted_at_utc": "2026-03-19T00:00:00Z",
  "registration": {
    "registrant_id": "reg_example_001",
    "full_name": "Your Name",
    "email": "you@example.com",
    "organization": "Your Org",
    "role": "Security Researcher"
  },
  "submission": {
    "submission_id": "sub_example_001",
    "registrant_id": "reg_example_001",
    "session_type": "talk",
    "title": "Your Session Title",
    "abstract": "One clear paragraph describing the technical content and practical value.",
    "audience_level": "advanced",
    "preferred_duration_minutes": 20
  }
}
```

## Review Criteria (Prototype)

- Relevance to DeFi security
- Technical rigor
- Practical applicability
- Evidence quality / reproducibility
- Clarity

## Author Checklist

- Session format matches content depth.
- Claims are backed by concrete examples or artifacts.
- Abstract is specific, not marketing copy.
- Links are accessible.
- Submission and registration IDs are consistent.

## Notes

- This is the current prototype spec.
- Double-blind review and expanded reviewer feedback forms are planned next.
