---
name: telegram-codex-cockpit
description: "Builds or maintains a Telegram-based Codex cockpit: a dedicated supergroup with topics, a bound OpenClaw agent, working /cas_* commands, and a clean topic-per-workstream workflow. Use when someone wants a better Telegram interface for Codex than a single DM thread."
---

# telegram-codex-cockpit

Скилл для настройки и обслуживания Telegram-чата, где **один topic = один поток работы с Codex**.

## Когда использовать
Используй этот скилл, когда пользователь хочет:
- отдельный Telegram-чат под Codex
- topics / ветки вместо хаоса в одной личке
- выделенный agent под Telegram cockpit
- рабочие `/cas_*` команды внутри Telegram topics
- понятный онбординг для реального использования, а не только техдок
- воспроизводимый публичный runbook без приватных привязок

## Что делает скилл
1. Создаёт или обслуживает Telegram supergroup под Codex
2. Включает topics
3. Добавляет Telegram-бота и поднимает его в admin
4. Создаёт базовую структуру тем
5. Привязывает чат к отдельному OpenClaw agent
6. Проверяет `/cas_*` команды и inline-кнопки
7. Даёт понятный онбординг для ежедневной работы

## Базовая структура topics
По умолчанию использовать такую схему:
- Inbox / Triage
- Codex Control
- Runtime / Ops
- Product / Build
- Research / Scratch

Если у пользователя уже есть своя проектная структура — адаптировать, а не навязывать эту сетку.

## Правила работы
- **Один topic = один workstream**
- Не мешать несколько независимых задач в одной ветке
- `Codex Control` держать для bind/status/control
- Проектную работу вести в профильных topics
- При правках конфига помнить, что массивы вроде `bindings` могут перезаписываться целиком

## Быстрый сценарий для пользователя
1. Зайти в `Codex Control`
2. Отправить `/cas_resume`
3. Выбрать existing thread или `New`
4. После bind писать уже обычным текстом
5. Для новой отдельной задачи уходить в профильный topic

## Что проверить после настройки
1. Чат существует и topics включены
2. Бот — admin
3. Отдельный agent привязан к этому чату
4. `/cas_resume` и `/cas_status` отвечают
5. Inline-кнопки работают в topics
6. Онбординг не врёт о реальном UX

## References
- [Публичный онбординг на русском](references/onboarding-ru.md)
- [Публичный runbook](references/runbook.md)
- [Quick test checklist](references/quick-test-checklist.md)
- [Manual review checklist](references/manual-review-checklist.md)
- [Public/private split notes](references/public-private-split.md)

## Output contract
Когда этот скилл используется, вернуть:
1. структура cockpit
2. как пользователь начинает работу
3. какие `/cas_*` команды нужны ежедневно
4. какие конфиг-риски есть
5. что осталось operator-specific и не должно утекать в public
