\n\n# Создание словаря слов

Вы можете создать пользовательский словарь слов для взламывания паролей, когда вы знаете, как может выглядеть пароль, и думаете, что возможны вариации слов или фраз.

## Использование Hashcat

Используйте файл правил (находится в `/usr/share/hashcat/rules`)

Вы можете связывать эти правила вместе, чтобы создать более большой словарь слов. Я предпочитаю начинать с 3–4 идей пароля, специфичных для пользователя, которого я пытаюсь взломать, затем использовать `best64.rule` и `toggles1.rule` на результате.

[[Hashcat|Узнайте больше о Hashcat]]

### Тoggles

```bash
hashcat --force --stdout passwords -r /usr/share/hashcat/rules/toggles1.rule > passwordlist
```

### Best64 Rules
```bash
hashcat --force --stdout passwords -r /usr/share/hashcat/rules/best64.rule > passwordlist
```

## Очистка словаря слов

### Уникальные пароли

```bash
cat passwordlist | sort -u > passwordlist-unique
```

### По длине

```bash
cat passwordlist | awk 'length($0) > 7' > passwordlist-eight
```

### Проверка количества

Пропускайте вывод в `wc -l`, чтобы проверить, сколько записей в списке.

# Теги

#cheat-sheet #cryptography
