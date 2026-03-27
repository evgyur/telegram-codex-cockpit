# Публичный runbook — Telegram Codex Cockpit

Цель: поднять и обслуживать Telegram cockpit для Codex без приватных привязок к конкретному пользователю, чату или серверу.

## Что должно получиться
- отдельный Telegram supergroup
- topics включены
- бот добавлен и поднят в admin
- чат привязан к отдельному agent
- `/cas_*` отвечают внутри topics
- inline-кнопки работают не только в DM, но и в group/topics

## Preconditions
Перед началом проверь:
- OpenClaw жив и отвечает
- Telegram transport жив
- `openclaw-codex-app-server` установлен и enabled
- есть доступ на config patch / restart

## Upstream reference
Оригинальная реализация может быть закреплена в репо как submodule:
- `references/openclaw-codex-app-server`
Оригинальная реализация Codex App Server может быть закреплена как submodule:
- upstream: `https://github.com/pwrdrvr/openclaw-codex-app-server.git`

## Шаги поднятия
### 1) Создать Telegram supergroup
Создай отдельный чат под Codex work.

### 2) Включить topics
Нужен именно forum/topic workflow, иначе весь cockpit деградирует в один длинный поток сообщений.

### 3) Добавить бота и выдать admin
Бот должен видеть group messages и уметь работать с topics.

### 4) Создать отдельный agent
Не привязывай cockpit к `main`, если хочешь чистую изоляцию контекста и workspace.

### 5) Привязать чат к agent
Держи binding отдельным и проверяй, что он не сносит существующие bindings.

### 6) Включить кнопки в topics
Важно:
- `channels.telegram.capabilities.inlineButtons = "all"`

Если оставить `dm`, кнопки могут нормально работать только в личке, а не в group/topics.

### 7) Засеять онбординг
Нужно объяснить пользователю:
- где делать первый bind
- какие команды реально нужны
- что после bind можно писать обычным текстом

## Главный footgun
`gateway config.patch` по массивам может перезаписать весь массив, а не merge’ить его.

Критично для:
- `bindings`
- других list-based секций

Правило:
- сначала читать текущий config
- потом patch’ить массив осознанно
- после patch проверять, что старые bindings не исчезли
