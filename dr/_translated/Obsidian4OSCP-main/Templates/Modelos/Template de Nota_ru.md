---
icon: 🗒
target:
- ""
createdAt: "{{DATE}}"
imageNameKey: nota_<% tp.file.title.split(" ").join("_").toLowerCase() %>
tags: 
NoteRel:
---
### Связанные записи
```dataview

TABLE 
	file.name as "File"
WHERE
	econtains(NoteRel, [[Notas/<% tp.file.title %>]])
```

------
## Напоминания
- Как было выявлено?
- Как было использовано?
- Проверьте, есть ли у вас все необходимые доказательства?
## Описание

напишите описание
```
