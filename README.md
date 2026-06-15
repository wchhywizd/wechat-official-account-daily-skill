# WeChat Official Account Daily Skill

Codex skill for producing Chinese WeChat Official Account content systems: article writing, topic structures, refined layout, visual production guidance, HTML preview, and WeChat draft-box handoff when credentials are available.

## What It Supports

- WeChat Official Account articles and daily publishing workflows
- Nutrition explainers, fitness lifestyle content, business insights, trend commentary, case breakdowns, and Xiaohongshu-style image-text planning
- Audience-aware structure for 30+ educated readers: story, detail, refined layout, practical advice, and soft conversion hooks
- Cover and illustration guidance, including mobile-first cover checks
- Draft-box publishing workflow through WeChat Official Account APIs when AppID/AppSecret are configured locally

## Files

- `SKILL.md`: main skill instructions
- `references/content-structures.md`: templates for nutrition, business insight, trend commentary, case breakdowns, checklist posts, and image-text cards
- `references/layout-publish.md`: WeChat article layout and draft-box handoff workflow
- `references/image-production.md`: cover, infographic, and image-text generation guidance
- `agents/openai.yaml`: UI metadata

## Install

Copy this folder into your Codex skills directory:

```bash
cp -R wechat-official-account-daily-skill ~/.agents/skills/wechat-official-account-daily
```

Then invoke it as:

```text
Use $wechat-official-account-daily to create a WeChat article with structure, visuals, layout, and draft-box handoff.
```

## Notes

Do not commit WeChat Official Account secrets. Store `AppID`, `AppSecret`, and access tokens outside this repository.
