# telegram-codex-cockpit

Канонический public skill и runbook для Telegram Codex cockpit на базе OpenClaw + Codex App Server.

## Что это
Это не «просто бот в Telegram». Это рабочий cockpit:
- отдельный чат
- topics вместо каши
- отдельный agent
- `/cas_*` как control surface
- progress heartbeat для длинных run
- stall notice + nudge, если bridge замолкает
- после bind можно писать обычным текстом

## Для кого
Для тех, кто хочет работать с Codex из Telegram нормально, а не держать всё в одной бесконечной личке.

## Что внутри
- `SKILL.md` — когда и как использовать skill
- `references/onboarding-ru.md` — понятная инструкция для ежедневной работы
- `references/runbook.md` — как поднять и поддерживать cockpit
- `references/public-private-split.md` — что должно оставаться приватным
- `references/refactor-topology-2026-04-09.md` — как разложены canonical public, compat alias и private overlay

## Главное правило UX
**Один topic = один workstream.**

Если мешать несколько задач в одной ветке, cockpit быстро превращается в шум.

## Operator contract
Public cockpit считается здоровым, если:
- `/cas_*` работают внутри topics,
- inline-кнопки работают не только в DM,
- voice notes доходят до Codex как transcript,
- inbound files доходят до Codex как local path/context,
- длинный run не исчезает в тишине,
- финал, blocker и вопрос к пользователю сразу возвращаются в topic.

### Heartbeat / stall-recovery
- в активной задаче cockpit не должен молчать дольше 150 секунд;
- если run ещё идёт, в topic нужен короткий progress update;
- если два окна heartbeat подряд нет видимого результата, cockpit должен показать stall notice и попробовать nudge;
- финальный ответ не должен теряться во внутреннем состоянии bridge/runtime.

## Skill topology after refactor
- `telegram-codex-cockpit` = canonical public contract
- `chip-codex-tg-public` = compatibility alias для старых упоминаний и ссылок
- `chip-codex-tg` = private live overlay с `chipcdx`, chat id, runbook и live snapshot

## Plugin reference
- `references/openclaw-codex-app-server` — optional pinned public submodule to `https://github.com/pwrdrvr/openclaw-codex-app-server.git`
- если submodule checkout'нут, использовать его как implementation reference для `/cas_*`, binding и bridge-layer
- если submodule не checkout'нут, upstream URL всё равно остаётся канонической public reference

## Важно
Этот public repo специально очищен от live/private привязок.

Здесь нет:
- реальных chat IDs,
- персональных agent IDs из боевого контура,
- локальных runtime paths конкретного сервера,
- приватных операторских деталей, которые относятся только к одному live setup.

Именно поэтому его можно держать публичным, не утаскивая с собой внутренний cockpit state.
