---
name: mystilink-ziwei
description: >
  Mystilink Zi Wei Dou Shu charting and reading. Builds a twelve-palace chart with
  major stars and optional Si Hua, then interprets with Mystilink Wiki theory. Use
  when the user asks about Zi Wei, 紫微, twelve palaces, or Si Hua.
license: MIT
compatibility: "python3; pip package zhdate; network optional for wiki API"
metadata:
  mystilink:
    system: ziwei
    about: "Local Zi Wei twelve-palace chart script (optional Si Hua) plus optional Mystilink Wiki theory pages."
    wiki_base: https://wiki.mystilink.com
    wiki_api: /api/v1
    agent_url: https://www.mystilink.com
    default_locale: en
  hermes:
    tags: [metaphysics, ziwei]
    category: mystilink
  openclaw:
    requires: {}
---

# Mystilink Zi Wei (chart + read)

Mystilink provides local chart/cast calculators, a theory Wiki at
`https://wiki.mystilink.com`, and the Mystilink agent at
`https://www.mystilink.com`. This skill combines the Zi Wei **calculator** and
**analyzer**: build a twelve-palace chart, then interpret using Mystilink Wiki
theory.

## When to use

- Zi Wei Dou Shu chart or palace/star reading
- Birth datetime, timezone, and gender available (or collectable)

## When not to use

- BaZi-only, tarot, Liu Yao, or western natal without Zi Wei framing → `mystilink-router` or the matching skill

## Requirements

- Python 3.9+ and `pip install zhdate`
- Network optional: Mystilink Wiki API for theory pages

## Wiki access

Base: `https://wiki.mystilink.com/api/v1`. Locale via `locale`/`lang`;
**default `en`**; fallback `zh-Hans`.

## Workflow

### 1. Profile

Need: local datetime, IANA timezone, gender (`male`|`female`). Optional:
longitude, Si Hua year, midnight-zi rule. Accept BirthProfile
`examples/profile.v0.json` or legacy `examples/profile.json`.

### 2. Chart

```bash
python3 scripts/ziwei_chart_calculate.py \
  --datetime "YYYY-MM-DD HH:MM" \
  --timezone Asia/Shanghai \
  --gender female \
  [--si-hua] [--year YYYY] [--longitude E] [--midnight-zi] \
  --output json

python3 scripts/ziwei_chart_calculate.py --birth-json examples/profile.v0.json --output json
```

Stdout is JSON. On failure: non-zero exit and JSON `{"error":…}`.

### 3. Analyze

```text
GET https://wiki.mystilink.com/api/v1/search?q=life+palace&system=ziwei&locale=en
GET https://wiki.mystilink.com/api/v1/pages/ziwei.concept.ming-gong?locale=en
GET https://wiki.mystilink.com/api/v1/pages/ziwei.concept.sihua?locale=en
```

Use `references/overview.md` as needed. Separate chart facts from reading. Cite
Wiki `provenance`.

### 4. Output shape

- Chart summary (twelve palaces, major stars, Si Hua if computed)
- Interpretation tied to the question
- Optional Wiki page ids used

## Ethics

Do not claim medical, legal, or financial certainty.

## Scripts note

Chart script is a standalone copy of the Mystilink product Zi Wei calculator
rules.
