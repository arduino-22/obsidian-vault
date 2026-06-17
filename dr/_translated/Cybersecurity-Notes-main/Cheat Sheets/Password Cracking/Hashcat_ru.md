
# Hashcat

Отличный учебник доступен [здесь](https://resources.infosecinstitute.com/topic/hashcat-tutorial-beginners/)

Рекомендуется обрабатывать хеш на своем хост-компьютере, а не в виртуальной машине. Если у вас есть Windows-хост-компьютер, установка Windows Subsystem for Linux может быть полезна. Облачные вычисления также могут быть полезны, хотя и дороги.

## Основная синтаксис

```bash
hashcat -m 0 -a 0 -o cracked hashes /usr/share/wordlists/rockyou.txt
```

Где `-o` указывает на выходной файл, `-a 0` указывает режим словаря, а `-m 0` — режим 0 (MD5).

Hashcat выдаст следующий результат, с выражением `Status: Cracked` (успех) или `Status: Exhausted` (неудача):

```bash
HASH:CRACKED_PASS
                                                 

Session..........: hashcat
Status...........: Cracked
Hash.Name........: HASH_TYPE
Hash.Target......: HASH
Time.Started.....: Sat Apr  3 14:55:24 2021 (8 secs)
Time.Estimated...: Sat Apr  3 14:55:32 2021 (0 secs)
Guess.Base.......: File (/usr/share/wordlists/rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:       46 H/s (10.53ms) @ Accel:32 Loops:1024 Thr:1 Vec:4
Recovered........: 1/1 (100.00%) Digests
Progress.........: 256/14344385 (0.00%)
Rejected.........: 0/256 (0.00%)
Restore.Point....: 224/14344385 (0.00%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:31744-32768
Candidates.#1....: tiffany -> freedom
```

Если вы получите ошибку `Separator unmatched`, это, вероятно, означает, что Hashcat ожидает какой-то разделительный символ (обычно точку с запятой `:`) в вашем хэше. Это значит, что вы выбрали неверный режим, и нужно выбрать другой.

## Выбор режима

Выполните этот команду, чтобы увидеть список примеров хэшей Hashcat.

```bash
$ hashcat --example-hashes
```

Этот список также доступен [здесь](https://hashcat.net/wiki/doku.php?id=example_hashes)

Вы можете искать в списке с помощью `grep` для находить хэши, похожие на ваш:

```bash
$ hashcat --example-hashes | grep '[PORTION OF HASH]' -B 3
```

Флаг `-B 3` показывает последние 3 строки перед совпадением. Это дает детали `MODE` и имя алгоритма.

**Добавьте примечания по использованию регулярных выражений здесь.**

Посмотрите справочник [[Идентификация хэшей]] для дополнительных техник.

# Теги

#cheat-sheet #cryptography
