**Подсистема Windows для Linux (WSL)** позволяет разработчикам запускать среду GNU/Linux с большинством программ командной строки, служебных программ и приложений непосредственно в Windows без каких-либо изменений и необходимости использовать традиционную виртуальную машину или двойную загрузку.

[WSL Команды](https://learn.microsoft.com/ru-ru/windows/wsl/basic-commands)

`/mnt` - директория с разделами windows

Команды:
- `wsl --install`, `wsl --install -d <Distribution Name>` - Установите WSL и дистрибутив Ubuntu по умолчанию для Linux.
- `wsl --list --verbose` - Список установленных дистрибутивов Linux
- `wsl --list --online` - Список доступных дистрибутивов Linux
- `wsl --status` - Проверка состояния WSL
- `wsl --version` - Проверка версии WSL
- `wsl --help` - Команда help
- `wsl --shutdown` - Shutdown
- `wsl --terminate <Distribution Name>` - Завершение
- `wsl -l -v` - узнать версию системы
- `wsl --install -d <Distribution Name>` - изменить установленный дистрибутив

## Перенос WSL на другой диск 

1) Экспорт нужной WSL
```
  wsl --export Ubuntu-18.04 "d:\ubuntu.tar"
```
2) Удаление контейнера
```
wsl --unregister Ubuntu-18.04
```
3) Импорт WSL
```
wsl --import Ubuntu-18.04 "e:\ubuntu1804-root" "d:\ubuntu.tar" --version 2
```
4) Запуск WSL
```
wsl -d Ubuntu-18.04
```
5) Установка пользоваетля по умолчанию
```
  sudo vim /etc/wsl.conf
```
Добавить в wsl.conf
```
[user]
default=user1
```
6) Перезагрузка WSL
```
wsl --shutdown
```

Обратить внимание: при установке wsl проверить в terminal установленный дистрибутив ubuntu. Снять галочку с пункта "Скрытие профиля из выпадающего списка"

Источник:
```
https://shra.ru/2022/03/perenos-ubuntu-wsl-na-drugojj-disk/
```
