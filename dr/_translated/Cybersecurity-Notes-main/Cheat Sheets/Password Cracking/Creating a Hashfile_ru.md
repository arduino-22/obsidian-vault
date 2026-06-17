# Создание файла хеша

## Добавление хеша

```bash
echo -n HASH >> hashes
```

Флаг `-n` удаляет последний новый строку

## Удаление последних новых строк

**Удалить один:**

```bash
truncate -s $(($(stat -c '%s' hashes)-1)) hashes
```

**Удалить все:**

```bash
sed -i 's/$//' hashes
```

# Теги

#cheat-sheet #cryptography
