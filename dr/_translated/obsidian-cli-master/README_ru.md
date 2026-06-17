# obscli

[![Crates.io](https://img.shields.io/crates/v/obscli?style=flat-square&logo=rust)](https://crates.io/crates/obscli)
[![Rust](https://img.shields.io/badge/rust-2024+-ed8225?style=flat-square&logo=rust&logoColor=white)](https://rust-lang.org)
[![License](https://img.shields.io/badge/license-MIT-22C55E?style=flat-square)](LICENSE)
[![Platform](https://img.shields.io/badge/platform-macOS%20·%20Linux-8B5CF6?style=flat-square)]()

English | [简体中文](README_CN.md)

[🐙 GitHub](https://github.com/trtyr/obsidian-cli) · [📦 crates.io](https://crates.io/crates/obscli) · [⚡ Quick Start](#-quick-start) · [📚 Commands](#-commands) · [🏗️ Architecture](#️-architecture)

**Быстрый CLI для Obsidian vault — работает без десктопного приложения.** Работает напрямую с файлами vault, имеет более 80 команд для управления заметками, ссылками, тегами, свойствами, задачами, ежедневными заметками, поиском, шаблонами, закладками и групповыми операциями. Создан на Rust с архитектурой микрокернела для максимальной расширяемости.

## 🆚 Почему obscli

|  | Obsidian CLI (Официальный) | obscli |
|---|---|---|
| **Зависимость от десктопа** | ❌ Требуется запуск приложения | ✅ Работает самостоятельно |
| **Структура команд** | ❌ Плоский набор имён | ✅ Вертикальная структура `ресурс действие` |
| **Групповые операции** | ❌ Ограничено | ✅ Полный CRUD для групп |
| **Обнаружение vault** | ❌ Ручное | ✅ Автоматическое обнаружение + конфигурация |
| **Отключённая работа** | ❌ Требует IPC | ✅ Прямой доступ к файлам |
| **Настройка** | ❌ Закрытая кодом | ✅ Микрокернела, расширяемая |

> **Ключевое отличие**: obscli рассматривает ваш vault как файловую систему, а не рабочий процесс — это позволяет автоматизации, интеграции CI/CD и работе без десктопа.

## 🚀 Установка

```bash
# Из crates.io (рекомендуется)
cargo install obscli

# Из исходников
git clone https://github.com/trtyr/obsidian-cli.git
cd obsidian-cli
cargo install --path .
```

## ⚡ Quick Start

```bash
# Установите ваш vault (однократное настройка)
obscli vault set "~/Documents/MyVault"

# Теперь используйте откуда угодно!
obscli vault info
obscli note list --recursive
obscli search "keyword"
obscli tag list --sort
```

## 📚 Команды

### Операции с заметками

```bash
obscli note create <name>           # Создать новую заметку
obscli note read <note>             # Прочитать содержимое заметки
obscli note edit <note>             # Открыть в $EDITOR
obscli note delete <note>           # Удалить заметку
obscli note move <src> <dest>       # Переместить/переименовать заметку
obscli note copy <src> <dest>       # Копировать заметку
obscli note list [path]             # Показать файлы
obscli note append <note> <text>    # Добавить текст к заметке
obscli note prepend <note> <text>   # Добавить текст в начало заметки
obscli note stats [note]            # Показать статистику
obscli note aliases <note>          # Показать aliasи
obscli note merge <s1,s2> <dest>    # Слив заметок
obscli note split <note> --level 1  # Разделить на заголовки
```

### Анализ ссылок

```bash
obscli link outgoing <note>         # Показать выходные ссылки
obscli link backlinks <note>        # Показать обратные ссылки
obscli link unresolved              # Показать неразрешённые ссылки
obscli link deadends                # Заметки без входных ссылок
obscli link orphans                 # Заметки без ссылок
obscli link rename <old> <new>      # Переименовать и обновить все ссылки
```

### Операции с тегами

```bash
obscli tag list                     # Показать все теги
obscli tag list --sort              # Сортировка по количеству
obscli tag notes <tag>              # Показать заметки с тегом
obscli tag add <note> <tag>         # Добавить тег в заметку
obscli tag remove <note> <tag>      # Удалить тег из заметки
obscli tag rename <old> <new>       # Переименовать тег во всех заметках
```

### Свойства frontmatter

```bash
obscli prop get <note>              # Показать все свойства
obscli prop get <note> <key>        # Показать конкретное свойство
obscli prop set <note> <key> <val>  # Установить свойство
obscli prop remove <note> <key>     # Удалить свойство
```

### Управление задачами

```bash
obscli task list [note]             # Показать задачи
obscli task list --pending          # Показать невыполненные задачи
obscli task add <note> <text>       # Добавить новую задачу
obscli task done <note> <line>      # Сделать задачу выполненной
obscli task undone <note> <line>    # Развернуть задачу
obscli task remove <note> <line>    # Удалить задачу
```

### Операции с ежедневными заметками

```bash
obscli daily.rs      # операции с ежедневными заметками
```

### Поиск

```bash
obscli search.rs     # поисковый команда
```

### Операции с шаблонами

```bash
obscli templates.rs  # операции с шаблонами
```

### Операции с закладками

```bash
obscli bookmarks.rs  # операции с закладками
```

### Групповые операции

```bash
obscli batch.rs      # групповые операции
```

### Другие функции

```bash
obscli misc.rs       # информация о vault, статистика, ремонт, установка, список, контур, сложность
```

## 🔧 Создание

- **Rust** ≥ 1.85 (edition 2024)
- **Не требуется C-библиотека** — obscli — чистый Rust

```bash
# Отладочная сборка
cargo build

# Распространённая сборка
cargo build --release

# Локальная установка
cargo install --path .
```

## 📄 Лицензия

MIT

---

⭐ Нравится этот материал? Ставьте звезду на [GitHub](https://github.com/trtyr/obsidian-cli).
