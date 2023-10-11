## Linux terminal shh(secure shell connection) connection

Программы для подключения через ssh

`putty` - одна из программ для подключения по ssh для windows
`mobaXterm` - одна из программ для подключения по ssh для windows

Как проверить создан ли ssh ключ:\
*В директории `~/.ssh/` проверить наличие файлов id_rsa.pub и id_rsa (стандарные имена для ключей)*

Скопировать ssh сгенерированный ключ для того, чтобы сервер его сохранил и входить можно было без пароля:
```
 ssh-copy-id -i ~/.ssh/id_rsa.pub user@remotehost

где:
    user – пользователь, под которым вы подключаетесь на удалённую машину;
    remotehost – ip-адрес удаленной машины.
    -i - опция указывает путь к вашему публичному ключу, который мы хотим закинуть на удаленный сервер

```

Полезные команды:
- `service ssh status` - узнать статус ssh сервиса
- `sudo apt-get install openssh-server` - установить openssh-server если не установлен
- `service ssh start` - стартануть сервер, есть не активен
- `ssh username@ipAddress` - подключится к компьютеру
- `ssh-keygen -t rsa` - сгенерировать публичный и приватный ключи (открытый id_rsa.pub и закрытый id_rsa)


Источники:
- [Создание public & private rsa ключей](https://jeka.by/ask/183/generate-ssh-keys/)
- [Настройка соединения с помощью rsa ключей public & private](https://jeka.by/ask/182/ssh-without-password/)
- [Настройка ssh config для входа по имени, а не по ip](https://blog.sedicomm.com/2018/04/08/kak-nastroit-polzovatelskoe-podklyucheniya-ssh-dlya-uproshheniya-udalennogo-dostupa/)
