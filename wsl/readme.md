**Подсистема Windows для Linux (WSL)** позволяет разработчикам запускать среду GNU/Linux с большинством программ командной строки, служебных программ и приложений непосредственно в Windows без каких-либо изменений и необходимости использовать традиционную виртуальную машину или двойную загрузку.

[WSL Команды](https://learn.microsoft.com/ru-ru/windows/wsl/basic-commands)

Команды:
- `wsl --install`, `wsl --install <Distribution Name>` - Установите WSL и дистрибутив Ubuntu по умолчанию для Linux.
- `wsl --list --verbose` - Список установленных дистрибутивов Linux
- `wsl --list --online` - Список доступных дистрибутивов Linux
- `wsl --status` - Проверка состояния WSL
- `wsl --version` - Проверка версии WSL
- `wsl --help` - Команда help
- `wsl --shutdown` - Shutdown
- `wsl --terminate <Distribution Name>` - Завершение