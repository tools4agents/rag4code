# Secrets Context

## Назначение

Этот файл фиксирует project-local правила для secret handling, local-only files и sanitized logging.

## Secret Surfaces

- `.env`
- <other local secret files>
- logs, если они могут содержать masked или accidental secret fragments

## Current Local Secret Baseline

- `<secret>` хранится в `<local file or env>`.
- `<file>` является local-only file.
- Example files могут содержать только placeholders.

## Rules

- Никогда не коммить реальные секреты.
- Не вставляй полный secret value в docs, tasks, ADR или reports.
- В логах и markdown artifacts используй только masked representation.

## Local Files Policy

- Temporary local artifacts допустимы, если они не содержат реальные секреты.
- Логи перед commit должны быть sanitized.
- Не ссылайся здесь на iteration-specific task artifacts.
