# Changelog

Version is tracked in `SKILL.md` under `metadata.mystilink.version` and in this file.

## 0.1.0

- Agent Skill for Zi Wei Dou Shu (twelve-palace) charting and reading
- `scripts/ziwei_chart_calculate.py` emits the chart JSON, with optional Si Hua
- `references/overview.md` maps palaces and stars to Mystilink Wiki theory pages (`wiki.mystilink.com`)
- `examples/profile.json` and `examples/profile.v0.json` give runnable chart input
- Runtime: `python3` with the `zhdate` package; the Wiki lookup is optional
- Install by copying this directory into a host skills path that reads `SKILL.md`
