# Загрузка файла

## Магические байты

**Просмотр магических байт**
```bash
head -c 20 /path/to/file | xxd
```

**Добавление магических байт в файл**

Добавьте магические байты безопасного файла (например, png) в пустой небезопасный файл:
```bash
head -c 8 /path/to/safe/file > unsafe\_file
```

Или объедините файл и хранимые магические байты:
```bash
cat /path/to/magic/bytes /path/to/file > new_file
```

# Теги

#cheat-sheet #web
