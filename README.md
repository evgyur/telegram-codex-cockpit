# telegram-codex-cockpit

Публичный skill и runbook для Telegram Codex cockpit на базе OpenClaw + Codex App Server.

## Что это
Это не "просто бот в Telegram". Это рабочий cockpit:
- отдельный чат
- topics вместо каши
- отдельный agent
- `/cas_*` как control surface
- после bind можно писать обычным текстом

## Для кого
Для тех, кто хочет работать с Codex из Telegram нормально, а не держать всё в одной бесконечной личке.

## Что внутри
- `SKILL.md` — когда и как использовать skill
- `references/onboarding-ru.md` — понятная инструкция для ежедневной работы
- `references/runbook.md` — как поднять и поддерживать cockpit
- `references/public-private-split.md` — что должно оставаться приватным

## Главное правило UX
**Один topic = один workstream.**

Если мешать несколько задач в одной ветке, cockpit быстро превращается в шум.

## Upstream reference
- `references/openclaw-codex-app-server` — pinned submodule to `https://github.com/pwrdrvr/openclaw-codex-app-server.git`
