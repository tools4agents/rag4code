# Architecture Specification: Code Analysis Core

> **Status**: Draft
> **Date**: 2026-02-23
> **Context**: Общий компонент структурного анализа для `code-atlas` и `code-rag`.

## 1. Overview

`code-analysis-core` — это Python-библиотека, предоставляющая унифицированные инструменты для структурного анализа кода. Она служит единым источником правды для генерации идентификаторов узлов (`node_id`), определения границ сущностей (`range`) и обнаружения проектов.

**Цель**: Обеспечить консистентность данных между `code-atlas` (граф знаний) и `code-rag` (семантический поиск), исключив дублирование логики парсинга и идентификации.

## 2. Responsibilities

1.  **Project Discovery**: Обнаружение границ проектов (Root vs Nested) и применение правил игнорирования (`.gitignore`, `.kilocode`).
2.  **Structural Analysis**: Парсинг Python-кода (через `Griffe`) и извлечение иерархии символов (Module, Class, Function).
3.  **Identity Management**: Генерация стабильных `node_id` и `qualname`.
4.  **Source Access**: Чтение контента символов по их координатам.

## 3. API Reference

### 3.1. Models

```python
from pydantic import BaseModel
from typing import List, Optional, Literal

class Range(BaseModel):
    start_line: int
    end_line: int

class Symbol(BaseModel):
    node_id: str          # e.g., "func:src/auth.py:AuthService.login"
    type: Literal["module", "class", "function"]
    name: str             # e.g., "login"
    qualname: str         # e.g., "AuthService.login"
    path: str             # relative path, e.g., "src/auth.py"
    range: Range
    docstring: Optional[str] = None
    # Для функций
    args: Optional[List[str]] = None
    return_type: Optional[str] = None
    is_async: bool = False
    # Для классов
    bases: Optional[List[str]] = None

class ProjectScope(BaseModel):
    name: str
    root_path: str
    type: Literal["root", "nested"]
```

### 3.2. Core Functions

#### `discover_projects(root: str) -> List[ProjectScope]`
Сканирует директорию на наличие `.git` или `pyproject.toml` и возвращает список обнаруженных проектов.

#### `analyze_file(path: str, project_root: str) -> List[Symbol]`
Анализирует один файл и возвращает плоский список всех найденных в нём символов (включая модуль, классы, методы).

#### `analyze_project(project_root: str) -> Iterator[Symbol]`
Генератор, обходящий весь проект (с учётом ignore rules) и возвращающий символы.

#### `read_symbol_content(file_path: str, range: Range) -> str`
Безопасное чтение исходного кода символа по его границам.

## 4. Integration Patterns

### 4.1. Usage in `code-atlas`
*   **Graph Building**: Использует `analyze_project` для первичного построения графа. Преобразует `Symbol` в узлы графа NetworkX.
*   **API Implementation**:
    *   `get_structure`: Маппит результат `analyze_file` в дерево.
    *   `read_symbol`: Использует `read_symbol_content`.
*   **Push Events**: Генерирует payload для `code-rag`, используя поля `node_id`, `range` и контент из `Symbol`.

### 4.2. Usage in `code-rag`
*   **Smart Chunking**:
    *   Плагин `rag4code.chunker` (стратегия `code-aware`) использует `analyze_file` для разбиения файла на логические блоки (функции/классы).
    *   Каждый `Symbol` становится кандидатом на чанк.
*   **Validation**: При приёме push-событий может использовать `code-analysis-core` для валидации `node_id` (опционально).

## 5. Implementation Details

*   **Backend**: `griffe` (для Python).
*   **Ignore Logic**: Поддержка стандартных `.gitignore` + специфика `.kilocode`.
*   **Performance**: Библиотека должна быть stateless и максимально быстрой. Кеширование — ответственность потребителя.

## 6. Roadmap

*   **v0.1**: Поддержка Python (Griffe).
*   **v0.2**: Оптимизация чтения файлов (lazy loading).
*   **v1.0**: Стабильный API для multi-language расширений (через плагины или внешние сервисы).
