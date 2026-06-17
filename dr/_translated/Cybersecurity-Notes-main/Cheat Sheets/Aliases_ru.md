# Алиасы

## Полезные алиасы

Вот некоторые примеры личных алиасов, которые я использовал. Они позволяют быстро перейти в определенные репозитории и быстро открыть файлы.

```bash
# Запуск VPN-сервисов
alias htbvpn="sudo openvpn  ~/Documents/HTB\ Access/Twigonometry.ovpn"
alias ravpn="sudo openvpn  ~/Documents/HTB\ Access/release_arena_Twigonometry.ovpn "
alias thmvpn="sudo openvpn  ~/Documents/THM\ Access/Twigonometry.ovpn"
alias seshvpn="sudo openvpn  ~/Documents/HTB\ Access/shefesh.ovpn"

# Редактирование общих файлов
alias nanbash="nano  ~/.bashrc"
alias nanhosts="nano /etc/hosts"

# Запуск веб-сервера в директории enum
alias enumserve="cd  ~/Documents/enum; python3 -m http.server"

# Запуск ghidra, удаление файла кэша для устранения проблем при запуске
alias run-ghidra="rm -r  ~/.ghidra; /opt/ghidra/ghidra_9.2.2_PUBLIC/ghidraRun"

# Переход в общие директории
alias sesh-site="cd  ~/Documents/SESH/SeshWebsite"
alias sesh-serve="cd  ~/Documents/SESH/SeshWebsite; bundle exec jekyll serve"
alias raspictf="cd  ~/Documents/SESH/RaspiCTF"

# Запуск Obsidian
alias obsidian="~/Applications/Obsidian-0.11.9.AppImage --no-sandbox"
```

## Добавление алиасов

```bash
nano  ~/.bashrc
[...введите код и сохраните...]
source  ~/.bashrc
```

# Теги

#cheat-sheet
