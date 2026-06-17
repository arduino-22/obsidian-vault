# obscli

[![Crates.io](https://img.shields.io/crates/v/obscli?style=flat-square&logo=rust)](https://crates.io/crates/obscli)
[![Rust](https://img.shields.io/badge/rust-2024+-ed8225?style=flat-square&logo=rust&logoColor=white)](https://rust-lang.org)
[![License](https://img.shields.io/badge/license-MIT-22C55E?style=flat-square)](LICENSE)
[![Platform](https://img.shields.io/badge/platform-macOS%20·%20Linux-8B5CF6?style=flat-square)]()

английский | [китайский](README_CN.md)

[🐙 GitHub](https://github.com/trtyr/obsidian-cli) · [📦 crates.io](https://crates.io/crates/obscli) · [⚡ 快速开始](#-快速开始) · [📚 命令](#-命令) · [🏗️ 架构](#️-架构)

**Быстрый CLI-инструмент для Obsidian-репозитория — работает без десктоп-приложения.** Прямая работа с файлами репозитория, более 80 команд, охватывает заметки, ссылки, метки, атрибуты, задачи, дневник, поиск, шаблоны, закладки и массовые операции. Состроен на Rust, использует микроядерную архитектуру, высокоэкспоненциальный.

## 🆚 Почему выбирают obscli

|  | Obsidian CLI (оффicial) | obscli |
|---|---|---|
| **Десктоп-зависимость** | ❌ требуется запускаемое приложение | ✅ работает независимо |
| **Структура команд** | ❌ плоский пространство имён | ✅ иерархическое `ресурс действие` |
| **Массовые операции** | ❌ ограничено | ✅ полный массовый CRUD |
| **Определение репозитория** | ❌ ручное указание | ✅ автоматическое обнаружение + настройка |
| **Отключённая работа** | ❌ требуется IPC | ✅ прямой доступ к файлам |
| **Настройка** | ❌ закрытая | ✅ микроядерная, экспоненциальная |

> **Основное преимущество**: obscli рассматривает ваш репозиторий как файловую систему, а не процесс — обеспечивает автоматизацию, интеграцию CI/CD и работу без десктопа.

## 🚀 Установка

```bash
# Установка из crates.io (рекомендуется)
cargo install obscli

# Установка из исходного кода
git clone https://github.com/trtyr/obsidian-cli.git
cd obsidian-cli
cargo install --path .
```

## ⚡ 快速 начало

```bash
# Настройка репозитория (однократная настройка)
obscli vault set "~/Documents/MyVault"

# Теперь можно использовать в любом каталоге!
obscli vault info
obscli note list --recursive
obscli search "ключевое слово"
obscli tag list --sort
```

## 📚 Команды

### Операции с заметками

```bash
obscli note create <название>           # Создать новую заметку
obscli note read <заметка>             # Прочитать содержимое заметки
obscli note edit <заметка>             # Открыть в $EDITOR
obscli note delete <заметка>           # Удалить заметку
obscli note move <источник> <цель>        # Переместить/переименовать заметку
obscli note copy <источник> <цель>        # Копировать заметку
obscli note list [путь]             # Показать файлы
obscli note append <заметка> <текст>    # Добавить текст
obscli note prepend <заметка> <текст>   # Присвоить текст
obscli note stats [заметка]            # Показать статистику
obscli note aliases <заметка>          # Показать alias
obscli note merge <s1,s2> <цель>    # Слияние заметок
obscli note split <заметка> --level 1  # Разбить по заголовку
```

### Анализ ссылок

```bash
obscli link outgoing <заметка>         # Показать выходные ссылки
obscli link backlinks <заметка>        # Показать обратные ссылки
obscli link unresolved              # Показать неразрешённые ссылки
obscli link deadends                # Заметки без входных ссылок
obscli link orphans                 # Заметки полностью без ссылок
obscli link rename <старый> <новый> # Переименовать метку
```

### Операции с метками

```bash
obscli tag list                     # Показать все метки
obscli tag list --sort              # Сортировка по количеству
obscli tag notes <метка>             # Показать заметки с этой меткой
obscli tag add <заметка> <метка>        # Добавить метку
obscli tag remove <заметка> <метка>     # Удалить метку
obscli tag rename <старый> <новый>         # Переименовать метку в заметках
```

### Атрибуты Frontmatter

```bash
obscli prop get <заметка>              # Показать все атрибуты
obscli prop -h                         # Показать помощь
```

## 🏗️ Архитектура

```
src/
├── main.rs           # Вход, обнаружение репозитория + распределение команд
├── cli.rs            # Определение иерархических sub-команд clap
├── kernel/           # Основные модули (микроядерная)
│   ├── mod.rs        # Экспорт модулей
│   ├── vault.rs      # Распознавание конфигурации репозитория
│   ├── note.rs       # Модель данных заметок (frontmatter, wikilinks, метки, задачи)
│   ├── index.rs      # Индекс репозитория (by_name, tag_index, backlinks)
│   ├── search.rs     # Поисковый индекс (фильтр, регулярные выражения, метки)
│   ├── output.rs     # Форматирование вывода
│   ├── fs.rs         # Инструменты файловой системы
│   └── config.rs     # Управление конфигурацией
└── plugins/          # Функциональные модули (декларативные)
    ├── mod.rs        # Распределение команд между плагинами
    ├── files.rs      # Массовые операции CRUD заметок
    ├── links.rs      # Анализ ссылок + переименование
    ├── tags.rs       # list/notes/add/remove/rename меток
    ├── properties.rs # get/set/remove атрибутов
    ├── tasks.rs      # list/add/done/undone/remove задач
    ├── daily.rs      # операции с дневником
    ├── search.rs     # команды поиска
    ├── templates.rs  # операции с шаблонами
    ├── bookmarks.rs  # операции с закладками
    ├── batch.rs      # массовые операции
    └── misc.rs       # info/stats/repair/export/set/unset/list, outline, текстовый вывод
```

## 🔧 Сборка

- **Rust** ≥ 1.85 (edition 2024)
- **Не требуется C-библиотека** — obscli — это чистый Rust-проект

```bash
# Быстрая сборка
cargo build

# Распространённая сборка
cargo build --release

# Локальная установка
cargo install --path .
```

## 📄 Лицензия

MIT

---

⭐ Если полезно? Поставьте звезду на [GitHub](https://github.com/trtyr/obsidian-cli)!
