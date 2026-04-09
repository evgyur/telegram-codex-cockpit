# Refactor topology — 2026-04-09

## Goal
Убрать лишний public drift вокруг Telegram Codex cockpit, не потеряв более новый operator contract и не смешав public shell с private live-state.

## Split plan
- `telegram-codex-cockpit` оставить как **canonical public skill**
- перенести в него более новый heartbeat / stall-recovery contract
- `chip-codex-tg-public` превратить в **compatibility alias**, а не во второй competing public center
- `chip-codex-tg` оставить как **private live overlay** для `chipcdx`, chat id, operator runbook и implementation snapshot

## Backward-compat map
- старое public имя `telegram-codex-cockpit` -> остаётся каноническим
- старое public имя `chip-codex-tg-public` -> сохраняется как alias, чтобы не ломать старые ссылки, промпты и привычку
- private `chip-codex-tg` -> остаётся live truth для контура Chip

## Migration notes
- новые public правки сначала должны попадать в `telegram-codex-cockpit`
- alias не должен снова обрастать отдельной логикой и competing docs
- live/private детали нельзя переносить в public только ради «удобства»
- если меняется operator contract, нужно синхронно проверить canonical public skill и private overlay
- если docs расходятся с working prod behavior, править docs, а не ломать working contour под старый текст

## Prod-first note
Этот refactor не должен менять уже работающий прод-контур только ради красоты структуры.

Правило:
- working prod behavior — baseline
- private live overlay — operator truth
- canonical public skill — sanitised reusable contract
- public alias — compatibility shim

Иначе говоря: сначала сохранить то, что реально работает, и только потом упрощать схему вокруг него.

## Why this shape
Так схема остаётся понятной:
- один public центр правды,
- один private live центр,
- один compat shim для мягкого перехода.
